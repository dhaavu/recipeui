<template>
<div class="main">
   <div class="container">
        <div v-if="editRecipe" class="edit-form">
            <form v-on:submit="updateRecipe">
                <h2>Edit Recipe</h2>
                <div class="inputs">
                    <h3>Recipe Name:</h3>
                <input type="text" name="name" id="name" v-model="name">
                <h3>Procedure:</h3>
                <!-- <input type="text" name="procedure" id="procedure" v-model="procedure"> -->
               <textarea name="procedure" id="procedure"  rows="15" v-model="procedure" ></textarea>
                <h3>Image URL:</h3>
                <input type="text" name="url" id="url" v-model="url">
                <h3>Id:</h3>
                <input readonly type="text" name="id" id="id" v-model="id">
               
                </div>
                 <div class="action">
                    <Button :buttonText="'Save'" :backgroundColor="'crimson'"></Button>
                    <Button @click="cancelEdit" :buttonText="'Cancel'" :backgroundColor="'grey'"></Button>
            
                </div>
           </form>
        </div>
        <div v-if="editRecipe == false" class="read-view">
            <img :src="url" alt="" style="">
            <div class="title">
                <h2>{{name}}</h2>
                <span @click="editMode" class="material-icons material-icons-outlined">
                 edit
                </span>
            </div>
            
            <div class="procedure">
                <p>{{procedure}}</p>
            </div>
            <div class="ingredients">
            <h2>Ingredients:</h2>
                <div v-for="ingredient in ingredients" :key="ingredient.ingredient_id"> 
                    <ul>
                        <li>{{ingredient.ingredient}}</li>
                        <li class="right">{{ingredient.qty}}</li>
                        <li >{{ingredient.measure}}</li>
                    </ul>
                    
                </div>
            </div>
            
            
        </div>
    </div>
</div>
 
    

    
</template>
<script>
import Button from "../components/button.vue"; 

export default {
components:{
    Button
}, 

  props:{
      
  }, 
  data(){ 
        return {
            id: String, 
        name: String, 
        procedure: String, 
        url:String, 
        ingredients:Array, 
        editRecipe: false
        }
        
    }, 
    methods: {
        updateRecipe(e)
        {
            e.preventDefault();
            console.log(this.name, this. procedure, this.url); 
        }, 
        editMode(){
            this.editRecipe = true; 
        }, 
        cancelEdit()
        {
            this.editRecipe= false; 
        }
    }, 
    mounted(){
        fetch('http://localhost:4000/api/recipe/' + this.$route.params.id)
        .then(response => response.text())
        .then(data => {
            var res = JSON.parse(data); 
            res = res.recipe; 
            this.id=res.row_id; 
            this.name=res.name; 
            this.procedure = res.procedure; 
            this.url = res.url; 
            this.ingredients = res.ingredients; 
        }).catch(err => console.log("error getting data >> ", err )); 
        
    }
   
    
}
</script>

<style scoped>
.main{
    display: flex;
    justify-content: center;
}
.container{
    display: flex;
    justify-content: center;
    align-items: center;
    margin:30px 20px; 
    width:90%; 
  border-radius: 20px;
    border: .5px solid #1f1e1e;
    box-shadow: -0.5rem 0.5rem 2rem 0rem #0b0909; 
    flex-wrap: wrap;
   max-width: 800px;
   background: #272626;
   
}


.container img{
    width:90%; 
    max-width:800px; 
    border: solid .5px #1f1e1e;
    border: .5px solid #1f1e1e;
    box-shadow: -0.5rem 0.5rem 2rem 0rem #0b0909; 
   margin-top:20px; 
}

ul{
      display: grid;
  grid-template-columns: 50% 15% 15%;
   padding:0px 3rem; 
    gap: 10px; 


}

li{
    text-decoration: none;
    list-style: none;
    color:white; 
}

.right{
    text-align: right;
}

.procedure {
 text-align:left; 
 word-break:break-all;
 margin:20px; 
}
.procedure p{
    font-size: 24px;
}

 p::first-letter{
 font-size:80px;
 font-style: italic;
 text-transform: capitalize;
}

.ingredients{
    text-align: left;
}
.ingredients h2{
    padding:20px; 
}

.title {
    display: flex;
    justify-content: space-around;
    align-items: center;
}
input{
   
    height:30px; 
    font-size: 20px;
    border-radius: 5px;
    padding:10px 20px; 
}

textarea{
    font-family: inherit;
    font-size: 20px;
    border-radius: 5px;
    padding:10px 20px; 
}
.inputs{
   display:grid; 
   grid-template-columns: 30% auto;
   padding: 10px;
   width:90%; 
   text-align:right; 
   grid-row-gap:20px; 
   grid-column-gap:30px; 
   align-items: center;
   
}

.action{
    display:flex; 
    justify-content: space-around;
    gap:30px;
    margin:20px; 
}

.edit-form{
    width:90%; 
}

@media only screen and (max-width: 768px) {
    .inputs{
   display:grid; 
   grid-template-columns: auto;
   

   text-align:left; 
   grid-row-gap:5px; 
   grid-column-gap:10px; 
   align-items: center;
   
}
h3{
    margin-bottom:0px; 
}
}

</style>
