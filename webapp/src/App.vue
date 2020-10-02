<template>
  <div id="app">
    <p>{{ greeting }}</p>
    <p>token: {{ token }}</p>
    <p>This var comes from flask: {{ flaskGreeting }}</p>
    <button @click="getMe">GET REQUEST</button>
    <button @click="postMe">POST REQUEST</button>
    <button @click="putMe">PUT REQUEST</button>
    <button @click="getToken">GET TOKEN</button>
    <button @click="profile">PUT WITH TOKEN TO PROFILE</button>
    <hello-world></hello-world>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data: function() {
    return {
      greeting: "Hello, Vue!",
      flaskGreeting: "",
      token: "",
    };
  },
  methods: {
    getMe() {
      console.log("in getMe...");
      let url = "http://localhost:1000/greeting";
      fetch(url, {
        method: "GET",
      })
        .then((response) => {
          return response.json();
        })
        .then((resp) => {
          console.log(resp);
        })
        .catch((err) => {
          alert("Error: " + err.message);
        });
    },
    postMe() {
      console.log("in postMe...");
      let username = "tokenGlobal";
      let password = "unused";
      let url = "http://localhost:1000/poo";
      let data = {
        firstname: "LukiePie",
      };
      fetch(url, {
        method: "POST",
        // method: "PUT"
        // ,
        headers: {
          // "Content-Type": "text/plain",
          "Content-Type": "application/json",
          Authorization: "Basic " + btoa(username + ":" + password),
        },
        // //credentials: "same-origin"
        // credentials: "include",
        body: JSON.stringify(data),
      })
        .then((response) => {
          return response.json();
        })
        .then((resp) => {
          console.log(resp);
        })
        .catch((err) => {
          alert("Error: " + err.message);
        });
    },
    putMe() {
      console.log("in putMe...");
      let username = "tokenGlobal";
      let password = "unused";
      let url = "http://localhost:1000/poot";
      let data = {
        firstname: "LukiePie",
      };
      fetch(url, {
        method: "PUT",
        // method: "PUT"
        // ,
        headers: {
          // "Content-Type": "text/plain",
          "Content-Type": "application/json",
          Authorization: "Basic " + btoa(username + ":" + password),
        },
        // //credentials: "same-origin"
        // credentials: "include",
        body: JSON.stringify(data),
      })
        .then((response) => {
          return response.json();
        })
        .then((resp) => {
          console.log(resp);
        })
        .catch((err) => {
          alert("Error: " + err.message);
        });
    },
    getToken() {
      console.log("in getToken...");
      let username = "lfernandez";
      let password = "white";
      fetch("http://localhost:1000//api/token", {
        method: "GET",
        headers: {
          "Content-Type": "text/plain",
          Authorization: "Basic " + btoa(username + ":" + password),
        },
        //credentials: "same-origin"
        //credentials: "include"
      })
        .then((response) => {
          return response.json();
        })
        .then((resp) => {
          console.log(resp);
          this.token = resp.token;
          console.log(this.token);
          console.log(
            "Token returned and stored in local var (also look for it the console)"
          );
        })
        .catch((err) => {
          alert("Error: " + err.message);
        });
    },
    profile() {
      console.log("in profile...");
      let username = this.token;
      let password = "unused";
      let url = "http://localhost:1000/api/profile";
      let data = {
        firstname: "LukiePie",
      };
      fetch(url, {
        method: "PUT",
        // method: "PUT"
        // ,
        headers: {
          // "Content-Type": "text/plain",
          "Content-Type": "application/json",
          Authorization: "Basic " + btoa(username + ":" + password),
        },
        // //credentials: "same-origin"
        // credentials: "include",
        body: JSON.stringify(data),
      })
        .then((response) => {
          return response.json();
        })
        .then((resp) => {
          console.log(resp);
        })
        .catch((err) => {
          alert("Error: " + err.message);
        });
    },
  },

  created: async function() {
    const gResponse = await fetch("http://localhost:1000/greeting");
    const gObject = await gResponse.json();
    this.flaskGreeting = gObject.greeting;
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
