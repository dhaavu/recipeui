<template>
  <div class="home">
   <List :items="items"></List> 
   
  </div>
</template>

<script>
// @ is an alias to /src
import List from '../components/List'

export default {
  name: 'Home',
  components: {
    List
  }, 
  data(){
    return {
      items: [{url:'https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg', title:'Dosa', description:'Best Indian breakfast'},
              {url:'https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg', title:'Dosa', description:'Best Indian breakfast'},
              {url:'https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg', title:'Dosa', description:'Best Indian breakfast'},
              {url:'https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg', title:'Dosa', description:'Best Indian breakfast'}  
            ]
    }
  }
}
</script>
