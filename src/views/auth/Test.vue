<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <button @click="login" type="button" v-if="!user">Login with Microsoft</button>
    <button @click="callAPI" type="button" v-if="user">
      Call Graph's /me API
    </button>
    <button @click="logout" type="button" v-if="user">
      Logout
    </button>
    <h3 v-if="user">Hello {{ user.name }}</h3>
    <pre v-if="userInfo">{{ JSON.stringify(userInfo, null, 4) }}</pre>
    <p v-if="loginFailed">Login unsuccessful</p>
    <p v-if="apiCallFailed">Graph API call unsuccessful</p>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      msg: 'Welcome to Your Vue.js + MSAL.js App',
      userInfo: null,
      apiCallFailed: false,
      loginFailed: false
    }
  },
  computed: {
    user: function() {
      return this.$AuthService.getUser()
    }
  },
  methods: {
    callAPI() {
      this.apiCallFailed = false;
      this.$AuthService.getGraphToken().then(
        token => {
          this.$AuthService.getGraphUserInfo(token).then(
            data => {
              this.userInfo = data;
            },
            error => {
              console.error(error);
              this.apiCallFailed = true;
            }
          );
        },
        error => {
          console.error(error);
          this.apiCallFailed = true;
        }
      );
    },

    logout() {
      this.$AuthService.logout();
    },

    login() {
      this.$AuthService.login();
    }
  }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
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

button {
  margin: 15px;
}
</style>
