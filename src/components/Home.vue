<template>
  <div id="home">
  <h3>{{ msg }}</h3>
  <button @click="googleLogin" class='btn'>Google</button>
  <button @click="twitterLogin" class='btn'>Twitter</button>
  <!--<button @click="githubLogin" class='btn'>GitHub</button>-->
  <button @click="facebookLogin" class='btn'>Facebook</button>
  </div>
</template>
<script>
  export default {
  name: 'home',
  data () {
    return {
      msg: 'ログイン'
    }
  },
  methods: {
    googleLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.GoogleAuthProvider());
    },
    twitterLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.TwitterAuthProvider());
    },
    githubLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.GithubAuthProvider());
    },
    facebookLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.FacebookAuthProvider());
    },
  }
}
</script>
