<template>
  <div id="app">
    <custom-input
      :input="data"
      @input="update"
    />
    <custom-input
      :input="data"
      :type="'percent'"
      @input="update"
    />
  </div>
</template>

<script>
import CustomInput from "./components/customInput.vue";
export default {
  name: 'app',
  components: {
    CustomInput
  },
  data() {
    return {
      data: '25'
    }
  },
  methods: {
    update(val) {
      this.data = val
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
