<template>
  <span class="alert" :class="classes">{{ content }}</span>
</template>

<script>
  export default {
    name: 'Alert',
    props: [ 'classes', 'content' ]
  }
</script>

<style>

</style>
