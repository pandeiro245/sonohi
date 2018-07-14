<template>
  <div id="home">
  <h3>{{ msg }}</h3>
  <button @click="googleLogin">Google</button>
  <button @click="twitterLogin">Twitter</button>
  <!--<button @click="githubLogin">GitHub</button>-->
  <button @click="facebookLogin">Facebook</button>
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
    githubLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.GithubAuthProvider());
    },
    facebookLogin: function(){
      firebase.auth().signInWithRedirect(new firebase.auth.FacebookAuthProvider());
    },
  }
}
</script>
