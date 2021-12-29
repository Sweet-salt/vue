<template>
  <h1>{{reversedMsg}}</h1>
  
</template>

<script>

  export default{
    data(){
      return {
        msg: 'hello'
      }
    },
    computed: {
      reversedMsg() {
        return this.msg.split('').reverse().join('') 
      }
    },
    methods:{
      reverseMsg() {
        return this.msg.split('').reverse().join('')
      }
    }
}
</script>

<style>

</style>
