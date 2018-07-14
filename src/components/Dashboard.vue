<template>
<div class="dashboard">
<h1> エディター画面</h1>
ようこそ{{user.displayName}}さん
<button @click="logout"> ログアウト</button>

<div class="dashboardWrapper">
<input>
</div>

</div>
</template>
　
<script>
export default {
  name: 'dashboard',
  props: ['user'],
  data () {
    return {
      markdown: '',
    }
  },
  methods: {
    logout: function() {
      firebase.auth().signOut();
    },
  },
}
</script>
<style lang="scss">

</style>
