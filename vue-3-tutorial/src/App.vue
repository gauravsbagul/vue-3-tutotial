<template>
  <div id="app">
    @{{ user.userName }} - {{ fullName }} <strong>followers: </strong>
    {{ followers }}
    <button @click="followUser">follow</button>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        userName: "gauravsbagul",
        firstName: "gaurav",
        lastName: "bagul",
        emial: "g@gmail.com",
        isAdmin: true,
      },
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },
  watch: {
    followers(newFollowerCount, oldFollowerCOunt) {
      if (oldFollowerCOunt < newFollowerCount) {
        console.log(`Log: ~> ${this.user.userName} has gained the follower`);
      }
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
  },
  mounted() {
    this.followUser();
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
  display: flex;
  flex-direction: column;
  justify-items: center;
}
</style>
