<template>
  <div class="converter">
    <h2>{{ currencyA }} To {{ currencyB }}</h2>
    <input type="text" v-model="currencyA_value" v-bind:placeholder="currencyA" />
    <input type="button" value="Convert" v-on:click="convert" />
    <h2>{{ currencyB_value }}</h2>
  </div>
</template>

<script>
export default {
  name: "Converter",
  props: ["currencyA", "currencyB"],
  data: function() {
    return {
      currencyA_value: "",
      currencyB_value: 0
    };
  },
  methods: {
    convert() {
      let query = this.currencyA + "_" + this.currencyB;
      let apiKey = "fa5cd1f8e99952f94ec6";
      let url =
        "https://free.currconv.com/api/v7/convert?q=" +
        query +
        "&compact=ultra&apiKey=" +
        apiKey;

      fetch(url)
        .then(response => {
          return response.json();
        })
        .then(json => {
          let price = json[query].val;
          this.currencyB_value = (
            price * parseFloat(this.currencyA_value)
          ).toFixed(2);
        });
    }
  }
};
</script>

<style scoped>
.converter {
  padding: 20px;
  max-width: 300px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
}
</style>