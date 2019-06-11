<template>
  <div id="app">
    <div id="nav">
    </div>
    <router-view/>
  </div>
</template>
<style>

  .nav-item:hover{
    color: rgba(255, 0, 0, 0.849);
    background-color: #fafafa0a;
    transition: 0.7s;
  }

  .img {
    background-image: url('/public/assets/img/wpp_car_1.jpg')
  }

</style>
<script>
import { mapState } from 'vuex'
import { mapMutations } from 'vuex'

export default {
  name: 'app',
  computed: {
    ...mapState([
      'usuario'
    ])
  },
  methods: {
    ...mapMutations([
      'logout'
    ])
  }
}
</script>
