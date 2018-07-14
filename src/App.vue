<template>
  <div id="app">
    <img src="https://ruffnote.com/attachments/56117" width="320px" />
    <h1>{{ msg }}</h1>
    <p>あと{{remain}}日00時間00分00秒。</p>
    <p>このサイトは西小倉宏信が<br>その日までに3つの目標を達成するために<br />
    たくさんの人を巻き込むことを目的としています。</p>
    <h3>1. 10万人からの「ありがとう」を集める</h3>
    <table>
    <tr>
      <th>18</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
      <th>22</th>
    </tr>
    <tr>
      <td>1</td>
      <td>3</td>
      <td>6</td>
      <td>8</td>
      <td>10</td>
    </tr>
    </table>
    <h3>2. 100人の年収を1,000万円以上にする</h3>
    <p>雇用形態（正社員・業務委託）は問わない</p>
    <table>
    <tr>
      <th>18</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
      <th>22</th>
    </tr>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>30</td>
      <td>70</td>
      <td>100</td>
    </tr>
    </table>

    <h3>3. 47都道府県に拠点を持つ</h3>
    <table>
    <tr>
      <th>18</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
      <th>22</th>
    </tr>
    <tr>
      <td>4</td>
      <td>10</td>
      <td>30</td>
      <td>40</td>
      <td>47</td>
    </tr>
    </table>


    <hr />
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

table {
  margin: 0 auto;
}
</style>
