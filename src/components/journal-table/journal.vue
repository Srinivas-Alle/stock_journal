<template>
<div>
  <div class="table journal">
    <v-btn @click="addStock" color="success">test</v-btn>
    <v-dialog
        max-width="500px"
        v-model="showForm"
          hide-overlay
          scrollable>

         <model-form></model-form>

    </v-dialog>

    <table class="journal-table">
    <thead>
      <tr>
        <th v-for="key in gridColumns" :key="key"
          @click="sortBy(key)"
          :class="{ active: sortKey == key }">
          {{key}}
          <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'">
          </span>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(entry,rowIndex) in gridData" :key="entry.name">
        <td v-for="(key,cellIndex) in gridColumns" :key="key">
          <span v-if="cellIndex==0">{{rowIndex+1}}</span>
          <span v-else> {{entry[key]}}</span>
        </td>
      </tr>
    </tbody>
  </table>
  </div>


</div>

</template>
<script>

import modelForm from "../../components/form/form";

export default {
  props: {},
  data() {
    const sortOrders = {};
    // this.columns.forEach((key) => {
    //   sortOrders[key] = 1;
    // });
    return {

      sortKey: "ebc",
      sortOrders,
      showForm: false,
      quotes: [],
      gridColumns: [
        "s.no",
        "entry date",
        "quote",
        "instrument",
        "long/short",
        "entry price",
        "quantity",
        "entry chart",
        "entry technicals",
        "notes",
        "exit date",
        "exit price",
        "exit chart",
        "exti technicals",
        "exit notes",
        "other notes",
        "profit/loss"
      ],
      gridData: [
        { name: "Chuck Norris", power: Infinity },
        { name: "Bruce Lee", power: 9000 },
        { name: "Jackie Chan", power: 7000 },
        { name: "Jet Li", power: 8000 }
      ]
    };
  },
  methods: {
    getData() {
      console.log("ss");
    },
    sendData() {
      this.stockDetails.push({
        name: "srinivas"
      });
    },
    getResponse() {
      return this.quotes[0].name;
    },
    addStock() {
      this.showForm = true;
    }
  },
  mounted() {
    this.quotes = [
      {
        sCode: 50002,
        sId: "ABB",
        sName: "ABB India Limited",
        industry: "Heavvy Electricals",
        instrument: "Equity"
      }
    ];
  },
  components: {
    modelForm
  }
};
</script>
<style lang='less' scoped>
.journal {
  width: 100%;
  height: 100%;
  .journal-table {
    table-layout: fixed;
    width: 100%;
    border: 1px solid red;
    thead th {
      text-transform: capitalize;
    }
  }
}
</style>

