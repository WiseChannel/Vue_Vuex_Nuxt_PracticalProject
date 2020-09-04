<template>
  <div class="message">
    <h1>{{message}}</h1>
  </div>
</template>

<script>
  export default {
    props: {
      message: {      //передача через props
        type: String,
        required: true,
        default: 'дефолтное сообщение'
      }
    }
  }
</script>

<style lang="css" scoped>
  .message {
    padding: 20px;
    text-align: center;
  }
</style>
