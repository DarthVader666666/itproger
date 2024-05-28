<template>
    <h3>{{info}}</h3>
    <p>{{someInfo}}</p>

    <button type="button" @click="userData('Some new')">Send</button>
</template>

<style scoped>
  h3 {
    font-weight: lighter;
  }

  p {
    color:red;
  }

</style>
<script>
  export default{
    data(){
      return {
        info:'Title',
        someInfo: 'Anons of message'
      }
    },
    methods: {
      userData(word = 'New Test')
      {
        this.info = word;
      }

    }
  }
</script>