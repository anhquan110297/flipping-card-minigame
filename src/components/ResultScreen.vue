<script>
  export default {
      props : {
          startTime: {
              type: Number,
              default: 0
          },
          endTime: {
              type: Number,
              default: 0
          },
      },
      computed : {
          calResultTime() {
              return this.endTime - this.startTime;
          }
      }
  }
</script>

<template>
  <h1>Hi from result screen</h1>
  <h1>{{calResultTime}}</h1>
</template>

<style scoped>

</style>