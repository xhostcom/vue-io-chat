<template>
  <div id="app">
    <div class="header">
    <h1>Chatroom</h1>
    <p class="username">User Name: {{ username }}</p>
    <p class="online">Online: {{ users.length }}</p>
    </div>
   <h2>Hello</h2>
  </div>
</template>

<script>
import io from 'socket.io-client';
export default {
  name: 'App',
  components: {},
  data: function() {
    return {
      username: "",
			socket: io("http://localhost:3000"),
			messages: [],
			users: []
    }
  },
  methods: {
    joinServer: function () {
      this.socket.on('loggedIn', data => {
         this.messages = data.messages;
      })
    }
  },
  mounted: function () {
   this.username = prompt("What is your username?", "Anonymous");

     if (!this.username) {
			this.username = "Anonymous";
		}

		this.joinServer();
  }

}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin:0;
  padding:0;
}
#app {
display: flex;
flex-direction:column;
height: 100vh;
width : 100%;
max-width: 768px;
margin: 0 auto;
}
</style>
