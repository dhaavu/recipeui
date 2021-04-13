<template>
<div class="main">
   <div class="container">
        <div v-if="editShow" class="edit-form">
            <form v-on:submit="updateRecipe">
                <input type="text" name="name" id="name" v-model="name">
                <input type="text" name="procedure" id="procedure" v-model="procedure">
                <input type="text" name="url" id="url" v-model="url">
                <input type="text" name="id" id="id" v-model="id">
                <button type="submit">Save</button>
            </form>
        </div>
        <div class="read-view">
            <img :src="url" alt="" style="">
            <h2>{{name}}</h2>
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
// import recipe from '../components/recipeDetails';
export default {
//   components: { recipe }, 
  props:{
      editShow: {default: false}
  }, 
  data(){ 
        return {
            id: String, 
        name: String, 
        procedure: String, 
        url:String, 
        ingredients:Array
        }
        
    }, 
    methods: {
        updateRecipe(e)
        {
            e.preventDefault();
            console.log(this.name, this. procedure, this.url); 
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
</style>
