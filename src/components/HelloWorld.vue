<template>
  <h1>{{}}</h1>
  
</template>

<script>
export default {
  data() {
    return{
      count: 0
    }
  },
  methods: {
    increase() {
      this.count +=1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
