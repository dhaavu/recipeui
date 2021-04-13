<template>
  <Header  :menuItems="menuItems"> </Header>
  <router-view/>
</template>
<script>
import Header from './components/Header'

export default {
  name: 'Home',
  components: {
    Header
  }, 
  data(){
    return {
        menuItems: [{name: 'Home', path:'/'},
                {name: 'About', path:'/about'}
                ]
    }
  
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;

}
body{
  padding:0;
  margin: 0;
  background: #1a1919;
}

</style>
