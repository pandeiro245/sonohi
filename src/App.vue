<template>
  <div id="app">
    <Home v-if="!isLogin"></Home>
 　 <Dashboard v-if="isLogin" :user="userData"></Dashboard>
    <h1>{{ msg }}</h1>
    <p>現在：{{now_at}}</p>
    <p>その日まで：{{remain}}</p>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://chat.vuejs.org" target="_blank">Community Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>
</template>

<script>
import Home from './components/Home.vue';
import Dashboard from './components/Dashboard.vue';

let now_at = 'aaa'
let remain = 'bbb'

export default {
  name: 'app',
  data () {
    return {
      msg: '西小倉宏信のホームページ',
      isLogin: false,
      userData: null,
      now_at: now_at,
      remain: remain 
    }
  },
  components: {
    'Home': Home,
    'Dashboard': Dashboard
  },
	created: function() {
		firebase.auth().onAuthStateChanged(user => {
			console.log(user);
			if (user) {
				this.isLogin = true;
        this.userData = user;
			} else {
				this.isLogin = false;
        this.userData = null;
			};
		});
	}
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
