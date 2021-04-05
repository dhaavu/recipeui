<template>
  <Header logoName="brunch_dining" :menuItems="menuItems"> </Header>
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
  color: #2c3e50;

}
body{
  padding:0;
  margin: 0;
}

</style>
