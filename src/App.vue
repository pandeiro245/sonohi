<template>
<div id="app">
<a href='/'><img src="https://ruffnote.com/attachments/56117" width="320px" /></a>
<h1>{{ msg }}</h1>
<p>{{ targetDateStr }}からあと{{remain}}日。</p>
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
import moment from 'moment'

export default {
  name: 'app',
  data () {
    return {
      msg: '2022年05月11日。水曜日。',
      isLogin: false,
      userData: null,
      targetDateStr: null,
      remain: null,
    }
  },
  components: {
    'Visions': Visions,
    'Home': Home,
    'Dashboard': Dashboard,
  },
  created: function() {
    var targetKey = location.hash.slice(1)
    this.targetDateStr = moment(targetKey).format('YYYY年MM月DD日');
    var goal = parseInt(moment('20220522').format('x'))
    var target  = parseInt(moment(targetKey).format('x'))
    this.remain = parseInt((goal - target)/(24 * 60 * 60 * 1000))

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
