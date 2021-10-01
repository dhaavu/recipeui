<template>
<div>
     <div class="autocomplete">
      <input id="myInput" type="text" name="myCountry" placeholder="Country">
    </div>
   
    <div id="text">
        <ul class="list">
             <li v-for="item in ingredients" :key="item._id">
                {{ item.name }}
            </li>
        </ul>
  
    </div>
</div>
 

</template>

<script>
export default {
props:{
        buttonText:String,  
        backgroundColor: String
    }, 
data(){
    return {
        ingredients: Array
    }
}, 
beforeMount() {
     fetch('http://localhost:4000/api/ingredient').then (
         response => response.json()).then(
             data => {
                 console.log(data.ingredient[0].name)
                 this.ingredients = data.ingredient; 
             }
         )
         
     
},
}
</script>

<style>

</style>