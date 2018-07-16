<template>
<div id="app">
<a href='/'><img src="https://ruffnote.com/attachments/56117" width="320px" /></a>
<h1>{{ msg }}</h1>

<p>このサイトは西小倉宏信が<br>その日までに3つの目標を達成するために<br />
たくさんの人を巻き込むことを目的としています。</p>



<Home v-if="!isLogin"></Home>
<Dashboard v-if="isLogin" :user="userData"></Dashboard>
<Visions></Visions>

</div>

</template>

<script>
import Visions from './components/Visions.vue';
import Home from './components/Home.vue';
import Dashboard from './components/Dashboard.vue';


export default {
  name: 'app',
  data () {
    return {
      msg: '2022年5月11日。水曜日。',
      isLogin: false,
      userData: null,
    }
  },
  components: {
    'Visions': Visions,
    'Home': Home,
    'Dashboard': Dashboard,
  },
	created: function() {
		firebase.auth().onAuthStateChanged(user => {
			console.log(user);
			if (user) {
				this.isLogin = true;
        this.userData = user;
        window.user = user
        localStorage['username'] = user.displayName;
        localStorage['uid'] = user.uid;
			} else {
				this.isLogin = false;
        this.userData = null;
			};
		});
	},
  // 処理
  methods: {
  }
}
</script>

<style lang="scss">
#app {
  text-align: center;
}

</style>
