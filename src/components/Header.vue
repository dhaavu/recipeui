<template>
<div class="header">
  <div class="brand">
    <a class="material-icons"> {{logoName}} </a>

  </div>
  <div class="menu">
    <ul>
      <li v-for="menuItem in menuItems" :key="menuItem.name">
      <router-link :to="{path: menuItem.path}">{{menuItem.name}}</router-link>
        
      </li>
      
    </ul>
  </div>
  <div class="profile">
    <a @click="expandMenu" class="material-icons">menu</a>
    <ul>
      <li>Register</li>
      <li> | </li>
      <li>Login</li>
    </ul>
    
    
   </div>
  


</div>

<div v-if="!isHidden" class="mobileMenu">
  <div v-for="menuItem in menuItems" :key ="menuItem.name">
     <router-link  :to="{path: menuItem.path}">{{menuItem.name}}</router-link>
  </div>
</div>

</template>

<script>
export default {
  name: 'Header',
  props: {
     menuItems: Array, 
      logoName: String 
  }, 
  data(){
    return {
     isHidden: true

    }
  }, 
  methods: {
    expandMenu(event){
      event.preventDefault(); 
      console.log("clicked"); 
      this.isHidden = !this.isHidden; 
    }, 
    
  }, 
  updated: function () {
    console.log("Mounted!!"); 
}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
  border-radius:50%; 
  border: white 1px solid; 
  cursor:pointer;
}

.header{
  background: #42b983; 
  display: flex; 
  justify-content:space-around;
  align-items: center;
  font-size: 18px; 
    box-shadow: 0 8px 6px 0px rgb(211, 211, 211);
}

.header >  div{
  text-align: center;
  /* border: 1px solid black; */
  
}

.header a { 
  font-size: 30px;
 margin:10px; 
  padding: 10px;
 box-shadow: -2rem 0 3rem -2rem #000;
}

.profile a{

  display: none;
}

.mobileMenu {
   box-shadow: 0 8px 6px 0px rgb(211, 211, 211);
  font-size: 18px;
  opacity: 1;
  animation:  opacityOn 5s normal forwards;
}

.menu a {
  text-decoration: none;
  color:#2c3e50;
  font-size: 20px;
  border:none;  
}

.mobileMenu a {
  text-decoration: none;
  color:white;
  font-size: 18px;
  border:none;  
}



@keyframes opacityOn {
    0% {
        opacity: 1;
    }
    25% {
        opacity: 0;
    }
    50% {
        opacity: 1;
    }
   
    100% {
        opacity: 1;
    }
}

.mobileMenu div{
  /* display: none; */
  padding:20px 5px; 
  background: rgb(43, 37, 37); 
  border-bottom: white 1px solid;
  color:white; 

}

@media only screen and (max-width: 768px) {
 .profile a{

  display: inline-block;
}
.profile ul{
  display:none; 
}
.menu {
  display: none;
}

.header{
  background: #42b983; 
  display: flex; 
  justify-content:space-between;
  align-items: center;
  font-size: 18px; 
  padding-left: 20px;
  padding-right: 20px; 
  box-shadow: 0 8px 6px 0px rgb(211, 211, 211);
}

}


</style>
