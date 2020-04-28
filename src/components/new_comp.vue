<template>
  <div id="about">
    <table class="table table-striped">
      <thead>
        <tr>
          <td>S.No#</td>
          <td>Product</td>
          <td>Cost</td>
          <td>Quantity</td>
          <td>Total</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(p, index) in products" :key="index">
          <td>1</td>
          <td>{{p.item}}</td>
          <td>{{p.cost}}</td>
          <td>
            <input
              type="number"
              class="form-control qty-box"
              name
              v-model.number="p.quantity"
              min="0"
            />
          </td>
          <td>{{p.cost*p.quantity}}</td>
        </tr>
      </tbody>
    </table>
    <div class="row">
      <div class="col-md-12">
        <p v-if="showButton">
          <button class="btn btn-success">Confirm</button>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "comp",
  data() {
    return {
      btn: false,
      counter: 8,
      qty: 0,
      proTotal: "",
      products: [
        { item: "timber", cost: 250, id: 1, quantity: 0 },
        { item: "wood", cost: 240, id: 2, quantity: 0 },
        { item: "primer", cost: 120, id: 3, quantity: 0 },
        { item: "plywood", cost: 360, id: 4, quantity: 0 },
        { item: "marker", cost: 220, id: 5, quantity: 0 },
        { item: "roughwood", cost: 480, id: 6, quantity: 0 }
      ],
      msg: "Counter"
    };
  },
  computed: {
    showButton() {
      var showButton = false;
      this.products.forEach(product => {
        if (product.quantity > 0) {
          showButton = true;
        }
      });
      return showButton;
    }
  }
};
</script>