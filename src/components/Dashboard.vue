<template>
<div class="dashboard">
ようこそ{{user.displayName}}さん
<button @click="logout"> ログアウト</button>

<h3>西小倉宏信にありがとうの気持ちを伝える</h3>
（開発中。開発できたら下記から登録できるようになるはず）
<br />
<input>

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
