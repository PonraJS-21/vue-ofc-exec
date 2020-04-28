<template>
  <div>
    <h1>{{ msg }}</h1>
    <div
      v-for="(data,i) in usrData.split(',')"
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
    <div v-if="!notSet">
      <input type="text" id="search-box" v-on:input="searchData" placeholder="search" />
    </div>

    <div id="master-list">
      <ol v-for="(filtredData,i) in filteredData" :key="'a'+i">
        <li v-on:click="setClickedValue">{{filtredData}}</li>
      </ol>
    </div>

    <div id="extra-component">
      <button v-on:click="setData">Set</button>
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
      notSet: true
    };
  },
  methods: {
    setData: function() {
      console.log("Set method");
      this.notSet = false;
      DB = this.strObj;
      console.log("DB: ", DB);

      //Hide old values
      document.getElementById("extra-component").style.display = "none";

      var allDiv = document.querySelectorAll("div[index]");
      allDiv.forEach(elem => {
        elem.style = "display: none";
      });
    },
    searchData: function() {
      if (this.notSet) return;

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
      document.getElementById("search-box").value = value;
      document.getElementById("master-list").style.display = "none";
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
  top: -15px;
  border: 1px solid grey;
  background-color: rgb(251, 253, 255);
  width: 200px;
  text-align: left;
  overflow: hidden;
  margin-left: auto;
  margin-right: auto;
}
input[type="text"] {
  width: 200px;
}
a {
  color: #42b983;
}
div {
  margin: 10px;
}
</style>
