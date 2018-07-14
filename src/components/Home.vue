<template>
  <div id="home">
  <h3>{{ msg }}</h3>
  <button @click="googleLogin">Google アカウントでログイン</button>
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
      console.log(1);
      firebase.auth().signInWithRedirect(new firebase.auth.GoogleAuthProvider());
      console.log(2);
    }
  }
}
</script>
