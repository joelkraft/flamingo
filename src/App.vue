<script>
import VueRouter from 'vue-router'

import Register from './components/Register.vue'
import Chart from './components/Chart.vue'

const routes = [
    { path: '/register', component: Register },
    { path: '/chart', component: Chart },
]
const router = new VueRouter({ routes })

export default {
  template: '<router-view :tableData="tableData"></router-view>',
  el: '#app',
  data: {
    tableData: [
        {
            name: 'Aardvark',
            color: 'green',
            food: 'flowers',
            size: 'medium',
        },
        {
            name: 'Caribou',
            color: 'brown',
            food: 'lichen',
            size: 'large',
        },
        {
            name: 'Fish',
            color: 'blue',
            food: 'fish food',
            size: 'small',
        },
        {
            name: 'Zebra',
            color: 'black and white',
            food: 'grass',
            size: 'large',
        },
        {
            name: 'Whale',
            color: 'blue',
            food: 'krill',
            size: 'huge',
        },
        {
            name: 'Dog',
            color: 'golden',
            food: 'beef',
            size: 'medium',
        }
    ]
  },
  router
}
</script>