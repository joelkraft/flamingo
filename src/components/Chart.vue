<template>
    <div class="section">
        <h1 class="title">{{heading}}</h1>
        <router-link to="register">To Register</router-link>
        <div class="level">
            <div class="container is-fluid">
                <ul>
                    <li v-for="row in tableData">{{row.name}}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
import '../libs/fa'
export default {
  data: function() {
    return {
        heading: 'Chart',
    }
  },
  props: ['tableData']
};
</script>