<template>
  <div id="home">
  <h3>{{ msg }}</h3>
  <button @click="googleLogin">Googleログイン</button>
  <button @click="twitterLogin">Twitterログイン</button>
  </div>
</template>
<script>
  export default {
  name: 'home',
  data () {
    return {
      msg: 'ログインして巻き込まれてみる'
    }
  },
  methods: {
    googleLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.GoogleAuthProvider());
    },
    twitterLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.TwitterAuthProvider());
    },
  }
}
</script>
