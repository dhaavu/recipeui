<template>
  <div class="home">
    
    <List :items="items"></List>

  </div>
</template>

<script>
// @ is an alias to /src
import List from "../components/List";
//const axios = require('axios');

export default {
  name: "Home",
  components: {
    List,
  },
  data() {
    return {
      responseData:'', 
      items: [],
    };
  },
  
    mounted() {
    fetch("https://zen-recipe.herokuapp.com/api/recipe")
      .then((response) => response.text()).then(data => {
        this.responseData = JSON.parse(data).recipe; 
        this.responseData.forEach(element => {
          this.items.push(element); 
        });
      })
      .catch((err) => console.log("error >>", err));
  },
}
  
  
</script>
