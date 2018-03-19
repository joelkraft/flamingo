<template>
  <router-view 
                    :table-data="tableData" 
                    v-on:changeTableData="updateTableData" 
                    v-on:createTransaction="createTransaction"
                    v-on:removeTransaction="removeTransaction"
                    v-on:sortColumn="sortByColumn"></router-view>
</template>

<script>
import VueRouter from 'vue-router'

import Register from './components/Register.vue'
import Chart from './components/Chart.vue'

import Utils from './Utils'
import './libs/fa'

import data from './data.json'

const routes = [
    { path: '/', component: {template: '<router-link to="register">Register</router-link>'} },
    { path: '/register', component: Register },
    { path: '/chart', component: Chart },
]
const router = new VueRouter({ routes })

export default {
  el: '#app',
  mounted: function() {
      this.tableData = data.data
  },
  data: {
    tableData: [],
    sortBy: {
        column: 'name',
        direction: false // true = up, false = down
    }
  },
  methods: {
      updateTableData: function({data, index, prop}) {
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
  router
}
</script>