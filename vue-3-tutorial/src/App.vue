<template>
  <div id='app'>
    <UserProfile/>
  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import UserProfile from './components/UserProfile'
export default {
  name: "App",
  components:{UserProfile}
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #f3F5FA;
}
</style>
