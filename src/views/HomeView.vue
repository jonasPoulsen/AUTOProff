<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Velkommen til din personale oversigt!</h1>
    <p>Ved at trykke "command" + "pil" til højre eller venstre, kan du navigere rundt i de forskellige sider!</p>
    <p> - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - </p>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
