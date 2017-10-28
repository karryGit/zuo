<template>

</template>

<script>
  import axios from 'axios';

  export default {
    name: '',
    data() {
        return{
          recoUsers:[]
        }
    },
    mounted() {
      axios.get('api/web_reco_users').then(function (response) {
          console.log(response)

      }).catch(function (err) {
        console.log(err);
      })
    }

  }
</script>

<style scoped>

</style>
