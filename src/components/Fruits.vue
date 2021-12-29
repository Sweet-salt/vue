<template>
  <section>
    <h1>Fruits</h1>
    <ul>
      <li
        v-for="fruit in fruits"
        :key="fruit"
      >
      {{fruits}}
      </li>
    </ul>
  </section>
</template>

<script>
  export default{
    data(){
      return{
        fruits: [
          'apple', 'banana', 'cherry'
        ]
      }
  }
}
</script>

<style scoped>

</style>
