<template>
  <table class="table is-striped">
    <thead>
      <tr>
        <th>&nbsp;&nbsp;&nbsp;Animal<span class="icon button is-light" style="float:right;" @click="sort('name')"><i class="fas fa-sort"></i></span></th>
        <th>&nbsp;&nbsp;&nbsp;Color<span class="icon button is-light" style="float:right;" @click="sort('color')"><i class="fas fa-sort"></i></span></th>
        <th>&nbsp;&nbsp;&nbsp;Food<span class="icon button is-light" style="float:right;" @click="sort('food')"><i class="fas fa-sort"></i></span></th>
        <th>&nbsp;&nbsp;&nbsp;Size<span class="icon button is-light" style="float:right;" @click="sort('size')"><i class="fas fa-sort"></i></span></th>
      </tr>
    </thead>
    <tbody>
      <NewTransaction v-on:createTransaction="createTransaction"></NewTransaction>
      <tr v-for="(item, index) in tableData">
        <Transaction :text="item.name" v-on:changeData="data => onChangeData({data, prop:'name', index})"></Transaction>
        <Transaction :text="item.color" v-on:changeData="data => onChangeData({data, prop:'color', index})"></Transaction>
        <Transaction :text="item.food" v-on:changeData="data => onChangeData({data, prop:'food', index})"></Transaction>
        <Transaction :text="item.size" v-on:changeData="data => onChangeData({data, prop:'size', index})"></Transaction>
        <td class="has-centered-text" style="vertical-align:middle;text-align: center;">
          <span class="icon button is-light" @click="handleRemove(index)">
            <i class="fas fa-times-circle is-large"></i>
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import NewTransaction from './NewTransaction.vue';
import Transaction from './Transaction.vue';

export default {
  components: {
    Transaction,
    NewTransaction,
  },
  props: ['tableData'],
  methods: {
    onChangeData: function({ data, index, prop }) {
      console.log('Transactions', data, index);
      this.$emit('changeTableData', { data, index, prop });
    },
    createTransaction: function(data) {
      this.$emit('createTransaction', data);
    },
    handleRemove: function(index) {
      this.$emit('removeTransaction', index)
    },
    sort: function(by) {
      this.$emit('sortColumn', by)
    }
  },
};
</script>
