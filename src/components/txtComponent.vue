<template>
  <div>
    <h1>{{ msg }}</h1>
    <!-- Displaying initial textboxes -->
    <div
      v-for="(data,i) in usrData.split(' ')"
      :key="data+i"
      v-bind:index="i"
      v-bind:style="styleObj"
    >
      <input
        type="text"
        v-bind:id="data.trim().toLowerCase()"
        v-model="strObj[i]"
        v-bind:placeholder="data.trim()"
      />
    </div>
    <!-- Set button -->
    <div id="extra-component">
      <button v-on:click="setData">Set</button>
    </div>
    <!-- search input field display none initially -->
    <div v-if="!notSet">
      <input
        type="text"
        id="search-box"
        v-on:input="searchData"
        placeholder="search"
        v-on:keydown="keyDown"
      />
    </div>
    <!-- search result list -->
    <div id="master-list">
      <ol id="u-order-list">
        <li
          v-for="(filtredData,i) in filteredData"
          :key="'a'+i"
          tabindex="-1"
          class="list-element"
          v-on:click="setClickedValue"
          v-on:keyup="setClickedValue"
          v-on:keydown="keyDown"
        >{{filtredData}}</li>
      </ol>
    </div>
  </div>
</template>

<script>
var DB;
export default {
  name: "txtComponent",
  props: {
    msg: String,
    usrData: String
  },
  data: function() {
    return {
      strObj: [""],
      filteredData: [],
      styleObj: {
        display: "block"
      },
      notSet: true,
      currListIndex: -1
    };
  },
  methods: {
    setData: function() {
      this.notSet = false;
      DB = this.strObj;

      //Hide old values
      document.getElementById("extra-component").style.display = "none";

      var allDiv = document.querySelectorAll("div[index]");
      allDiv.forEach(elem => {
        elem.style = "display: none";
      });
    },
    searchData: function() {
      this.filteredData = [];
      document.getElementById("master-list").style.display = "block";
      var searchInput = event.target.value,
        foundItem = DB.filter(item => {
          return item.includes(searchInput) && searchInput.trim() != "";
        });

      this.filteredData = foundItem;
    },
    setClickedValue: function() {
      var value = event.target.innerText;
      if (event.keyCode === 13 || event.type === "click") {
        //Resetting li focus index
        this.currListIndex = -1;
        //Set search box value
        document.getElementById("search-box").value = value;
        document.getElementById("master-list").style.display = "none";
      }
    },
    keyDown: function() {
      try {
        var ul = document.getElementById("u-order-list");
        var maxListLength = ul.childNodes.length;

        //Arrow down event
        if (
          event.code === "ArrowDown" &&
          this.currListIndex < maxListLength - 1
        ) {
          this.currListIndex = this.currListIndex + 1;
          this.setFocus(this.currListIndex, ul);
        } else if (event.code === "ArrowUp" && this.currListIndex > 0) {
          //Arrow Up event
          this.currListIndex = this.currListIndex - 1;
          this.setFocus(this.currListIndex, ul);
        }
      } catch (error) {
        //empty
      }
    },
    setFocus: function(focusIndex, ul) {
      var child = ul.childNodes[focusIndex];
      child.focus();
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: block;
  position: relative;
  left: -20px;
  top: -10px;
  border: 0.5px solid #41b883;
  text-align: left;
  overflow: hidden;
  margin-left: auto;
  margin-right: auto;
}
input[type="text"],
li {
  width: 200px;
  padding: 5px;
  font-size: 15px;
  border: 1px solid #35495e;
}
input[type="text"] {
  outline: none;
}
a {
  color: #42b983;
}
div {
  margin: 10px;
}
ol {
  margin: 0px;
}
button {
  background-color: #41b883;
  padding: 5px;
  color: white;
  width: 60px;
  border-radius: 4px;
  border: none;
}
li:focus,
li:hover {
  background-color: #41b883;
  color: white;
}
li:focus {
  border: 2px solid #35495e;
}
</style>
