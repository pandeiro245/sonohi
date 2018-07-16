<template>
<div id="app">
<img src="https://ruffnote.com/attachments/56117" width="320px" />
<h1>{{ msg }}</h1>
<p>あと{{remain}}日00時間00分00秒。</p>
<p>このサイトは西小倉宏信が<br>その日までに3つの目標を達成するために<br />
たくさんの人を巻き込むことを目的としています。</p>


<h3>1. 10万人からの「ありがとう」を集める</h3>
<table class='table table-bordered'>
<tr>
<th>2019</th>
<th>2020</th>
<th>2021</th>
<th>2022</th>
</tr>
<tr>
<td>0 / 20,000</td>
<td>0 / 40,000</td>
<td>0 / 60,000</td>
<td>0 / 100,000</td>
</tr>
</table>
<h3>2. 100人の年収を1,000万円以上にする</h3>
<p>雇用形態（正社員・業務委託）は問わない</p>
<table class='table table-bordered'>
<tr>
<th>2019</th>
<th>2020</th>
<th>2021</th>
<th>2022</th>

</tr>
<tr>
<td>0 / 3</td>
<td>0 / 30</td>
<td>0 / 70</td>
<td>0 / 100</td>
</tr>
</table>

<h3>3. 47都道府県に拠点を持つ</h3>
<table class='table table-bordered'>
<tr>
<th>2019</th>
<th>2020</th>
<th>2021</th>
<th>2022</th>
</tr>
<tr>
<td>4 / 10</td>
<td>4 / 30</td>
<td>4 / 40</td>
<td>4 / 47</td>
</tr>
</table>

<Home v-if="!isLogin"></Home>
<Dashboard v-if="isLogin" :user="userData"></Dashboard>
</div>
</template>

<script>
import Home from './components/Home.vue';
import Dashboard from './components/Dashboard.vue';

let now_at = 'aaa'
let remain = '1,397'

export default {
  name: 'app',
  data () {
    return {
      msg: '2022年5月11日。水曜日。',
      isLogin: false,
      userData: null,
      now_at: now_at,
      remain: remain,
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
