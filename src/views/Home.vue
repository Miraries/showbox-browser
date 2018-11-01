<template>
  <div class="container">
    <div class="row justify-content-center">
      <h1>In-browser Showbox</h1>  
    </div>
    <Search></Search>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'
import Search from '@/components/Search.vue'

export default {
  name: 'home',
  components: {
    //HelloWorld
    Search
  }
}
</script>
