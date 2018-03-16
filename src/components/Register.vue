<template>
    <div class="section">
        <h1 class="title">{{heading}}</h1>
        <router-link to="chart">Chart</router-link>
        <div class="level">
            <div class="container is-fluid">
                <Transactions 
                    :table-data="tableData" 
                    v-on:changeTableData="updateTableData" 
                    v-on:createTransaction="createTransaction"
                    v-on:removeTransaction="removeTransaction"
                    v-on:sortColumn="sortByColumn">
                </Transactions>
            </div>
        </div>
    </div>
</template>

<script>
import Utils from '../Utils'
import '../libs/fa'
import Transactions from './Transactions.vue'
export default {
  components: {
    Transactions,
  },
  methods: {
      updateTableData: function({data, index, prop}) {
                console.log('App', data, index, prop)
          this.tableData[index][prop] = data
      },
      createTransaction: function(data) {
          this.tableData.push(data)
      },
      removeTransaction: function(index) {
          this.tableData = this.tableData.filter((d,i) => i !== index)
      },
      sortByColumn: function(by) {
          this.sortBy.direction = this.sortBy.column === by ? !this.sortBy.direction : true
          this.sortBy.column = by
          Utils.sort(this.tableData, by, this.sortBy.direction)
      }
  },
  data: function() {
      return {
        heading: 'Numbers',
        sortBy: {
            column: 'name',
            direction: false // true = up, false = down
        }
    }
  },
  props: ['tableData']
};
</script>