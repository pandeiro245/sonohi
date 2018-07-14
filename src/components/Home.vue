<template>
  <div id="home">
  <img src="https://ruffnote.com/pandeiro245/avatar">
  <h1>{{ msg }}</h1>
  <p>みんなの「その日」をみんなで応援</p>
  <button @click="googleLogin">Google アカウントでログイン</button>
  </div>
</template>
<script>
  export default {
  name: 'home',
  data () {
    return {
      msg: 'Sonohi Cloud'
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
