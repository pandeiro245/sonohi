<template>
<div class="dashboard">
ようこそ{{user.displayName}}さん
<button @click="logout"> ログアウト</button>

<h3>どんな機能が欲しい？ここのチャットで話しましょう…！</h3>
<div id="message-contents">
<!-- ▼メッセージ一個ぶんの表示 -->
<div v-for="message in messageList" class="message-wrapper is-clearfix">
<div class="box" v-bind:class="{'mymessage' : isMyMessage(message) }">
<div class="content">
<p>
<strong>{{message.userName}}</strong> <small>{{displayTime(message)}}</small>
<br />
{{message.message}}
</p>
</div>
</div>
</div>
<!-- ▲メッセージ一個ぶんの表示 -->
</div>

<!-- ▼メッセージ入力部分 -->
<footer>
<div class="field is-grouped">
<div class="control is-expanded">
<input v-model="message" v-on:keydown.enter="send" class="input is-medium" type="text" placeholder="Message" />
</div>
<div class="control control-submit">
<button v-bind:disabled="message.length==0" v-on:click="send" class="button is-primary button-submit">送信</button>
</div>
</div>
</footer>
<!-- ▲メッセージ入力部分 -->

</div>
</template>
　
<script>
export default {
  name: 'dashboard',
  props: ['user'],
  data () {
    return {
      message: "",
      userName: localStorage['username'],
      userId: localStorage['uid'],
      messageList: [],
    }
  },
  created: function(){
    this.setupChat()
    this.loadMessage()
  },
  methods: {
    logout: function() {
      firebase.auth().signOut();
    },

    setupChat: function(){
      let hash = location.hash
      let ref = firebase.database().ref('chats')
      if(hash != null || hash.length == 0){
        hash = '20180716'
        location.hash = hash
      }
      this.chatRef = ref.child(hash)
    },

    send: function(event){
      if(this.message.length == 0){
          return;
      }

      let messageRef = firebase.database().ref('messages').push()
      let createdAt = this.timestamp()

      let chat = this.chatRef.key
      messageRef.set({
          chat: chat
          , message:this.message
          , userName: this.userName
          , userId: this.userId
          , createdAt: createdAt
          , createdAtReverse: -createdAt
      })
      this.message = ""
    },
    loadMessage:function(){
        let chatKey = this.chatRef.key
        let loadRef = firebase.database().ref("messages").orderByChild("chat").equalTo(chatKey)

        loadRef.once('value').then((snapshot) => {

            var messageList = []            
            snapshot.forEach(function(childSnapshot) {
                var data = childSnapshot.val()
                data.key = childSnapshot.key
                messageList.push(data)
            })
            messageList.sort(function(a,b){
                if( a.createdAt < b.createdAt ) return -1;
                if( a.createdAt > b.createdAt ) return 1;
                return 0;
            });

            this.messageList = messageList
            this.observeMessage()
            this.scrollToBottom()
        });
    },
    observeMessage: function(){
      let chatKey = this.chatRef.key
      let chatRef = firebase.database().ref("messages").orderByChild("chat").equalTo(chatKey)
      chatRef.on("child_added", (snapshot) => {
        let newMessage = snapshot.val()
        newMessage.key = snapshot.key
        for(var i=0,max=this.messageList.length;i<max;i++) {
          let message = this.messageList[i]
          if(message.key == newMessage.key){
            return
          }
        }
        this.messageList.push(newMessage)
        this.scrollToBottom()
      })
    },

    scrollToBottom :function() {
      setTimeout(()=>{
        let height = Math.max(0, document.body.scrollHeight - document.body.clientHeight)
        anime({
          targets: "body",
          scrollTop: height,
          duration: 200,
          easing: "easeInQuad"
        });
      }, 100)
    },

    isMyMessage: function(message){
      return this.userId == message.userId
    },

    displayTime: function(message) {
      let timestamp = message.createdAt * 1000
      var date = new Date(timestamp)
      var diff = new Date().getTime() - date.getTime()
      var d = new Date(diff);

      if (d.getUTCFullYear() - 1970) {
        return d.getUTCFullYear() - 1970 + '年前'
      } else if (d.getUTCMonth()) {
        return d.getUTCMonth() + 'ヶ月前'
      } else if (d.getUTCDate() - 1) {
        return d.getUTCDate() - 1 + '日前'
      } else if (d.getUTCHours()) {
        return d.getUTCHours() + '時間前'
      } else if (d.getUTCMinutes()) {
        return d.getUTCMinutes() + '分前'
      } else {
        return d.getUTCSeconds() + '秒前'
      }
    },
    timestamp: function(){
      let date = new Date()
      let timestamp = date.getTime()
      return Math.floor( timestamp / 1000 )
    }
  },
}
</script>
<style lang="scss">

</style>
