<template>
    <div>
        <h1>Hello {{ userName }}</h1>
        <p>{{message}}</p>
    </div>
</template>
<script>
export default {
  data() {
    return {
      userName: 'M-ur-phy',
      message: 'Welcome Vue world',
      arr: [],
      obj: {}
    }
  }
}
</script>
<style scoped>
.text-red  {
    color: red;
}
</style>
