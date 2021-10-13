<template>
<div class="main">
   <div class="container">
        <div  v-if="editRecipe == false && addIngredient == false"  class="read-view">
            <img :src="url" alt="" style="">
            <div class="title">
                <h2>{{name}}</h2>
                <span @click="editMode" class=" action-icon material-icons material-icons-outlined">
                 edit
                </span>
            </div>
             <div class="recipe-type">
               
                <h4>{{type}}</h4>
            </div>
            <div v-html="procedure" class="procedure">
               
            </div>
           
            
            <div class="ingredients">
            <div class="section">
                <h2>Ingredients: </h2>
                <span @click="addIngredients" class=" action-icon material-icons material-icons-outlined">
                 add
                </span>
            </div>
            
                <div v-for="ingredient in ingredients"  :key="ingredient.ingredient_id"> 
                    <ul>
                        <li>{{ingredient.ingredient}}</li>
                        <li class="right">{{ingredient.qty}}</li>
                        <li >{{ingredient.measure}}</li>
                        <li style="display:flex">
                            <span @click="deleteIngredient(ingredient.recipe_ingredient_id)" class=" action-icon material-icons material-icons-outlined">
                                delete
                            </span>
                            
                        </li>
                    </ul>
                    
                </div>
            </div>
            
            
        </div>

        <div v-if="editRecipe" class="edit-form">
            <form v-on:submit="updateRecipe">
                <h2>Edit Recipe</h2>
                <div class="inputs">
                    <h3>Recipe Name:</h3>
                <input type="text" name="name" id="name" v-model="name">
                <h3>Type</h3> 
                <!-- <input type="text" name="type" id="type" v-model="type"> -->
                <DxSelectBox
                    v-model="type"
                    :data-source="typeOptions"
                    value-expr="Name"
                    display-expr="Name"
                />
                <h3>Procedure:</h3>
                 <DxHtmlEditor  :allowfullscreen="true" value-type="html" v-model="procedure" :height="300"> 
                    <DxToolbar :multiline="isMultiline">
                        <DxItem format-name="undo"/>
                        <DxItem format-name="redo"/>
                        <DxItem format-name="separator"/>
                        <DxItem
                        :format-values="sizeValues"
                        format-name="size"
                        />
                        <DxItem
                        :format-values="fontValues"
                        format-name="font"
                        />
                        <DxItem format-name="separator"/>
                        <DxItem format-name="bold"/>
                        <DxItem format-name="italic"/>
                        <DxItem format-name="strike"/>
                        <DxItem format-name="underline"/>
                        <DxItem format-name="separator"/>
                        <DxItem format-name="alignLeft"/>
                        <DxItem format-name="alignCenter"/>
                        <DxItem format-name="alignRight"/>
                        <DxItem format-name="alignJustify"/>
                        <DxItem format-name="separator"/>
                        <DxItem format-name="orderedList"/>
                        <DxItem format-name="bulletList"/>
                        <DxItem format-name="separator"/>
                        <DxItem
                        :format-values="headerValues"
                        format-name="header"
                        />
                        <DxItem format-name="separator"/>
                        <DxItem format-name="color"/>
                        <DxItem format-name="background"/>
                        <DxItem format-name="separator"/>
                        <DxItem format-name="link"/>
                        <DxItem format-name="code"/>
                        <DxItem format-name="image"/>
                        <DxItem format-name="separator"/>
                        <DxItem format-name="clear"/>
                        <DxItem format-name="codeBlock"/>
                        <DxItem format-name="blockquote"/>
                        <DxItem format-name="separator"/>
                        <DxItem format-name="insertTable"/>
                        <DxItem format-name="deleteTable"/>
                        <DxItem format-name="insertRowAbove"/>
                        <DxItem format-name="insertRowBelow"/>
                        <DxItem format-name="deleteRow"/>
                        <DxItem format-name="insertColumnLeft"/>
                        <DxItem format-name="insertColumnRight"/>
                        <DxItem format-name="deleteColumn"/>
                    </DxToolbar>
                 </DxHtmlEditor>
                <!-- <input type="text" name="procedure" id="procedure" v-model="procedure"> -->
              <!-- <textarea name="procedure" id="procedure"  rows="15" v-model="procedure" ></textarea> -->
                <h3>Image URL:</h3>
                <input type="text" name="url" id="url" v-model="url">
                <h3>Id:</h3>
                <input readonly type="text" name="id" id="id" v-model="id">
               
                </div>
                 <div class="action">
                    <Button @click="updateRecipe" :buttonText="'Save'" :backgroundColor="'crimson'"></Button>
                    <Button @click="cancelEdit" :buttonText="'Cancel'" :backgroundColor="'grey'"></Button>
            
                </div>
           </form>
        </div>
        
        <div v-if="editRecipe == false && addIngredient == true" class="add-ing">
            
           
            <lookup @update="getIngredientLookup"> </lookup>
            <input type="text" name="quantity"  id="quantity" autocomplete="off" placeholder="Quantity" v-model="quantity">
            <select name="uom" id="uom" v-model="uom">
                <option value="gram">Grams</option>
                <option value="unit">Piece</option>
                <option value="cups">Cups</option>
                <option value="Table Spoon">Table Spoon</option>
                <option value="Tea Spoon">Tea Spoon</option>
                <option value="Pinch">Pinch</option>
            </select>
           <div class="actions">
                <Button class="button" @click="sendIngredient" :buttonText="'Save'" :backgroundColor="'crimson'"></Button>
                <Button class="button" @click="cancelAdd" :buttonText="'Cancel'" :backgroundColor="'grey'"></Button>
           </div>
          
        </div>
    </div>
</div>
 
    

    
</template>
<script>
import Button from "../components/button.vue"; 
import Lookup from "../components/lookup.vue"; 
import 'devextreme/dist/css/dx.common.css';

import 'devextreme/dist/css/dx.dark.css';
import { DxSelectBox } from 'devextreme-vue/select-box'; 
import { DxHtmlEditor, DxToolbar, DxItem,  } from 'devextreme-vue/html-editor';

export default {
components:{
    Button, 
    DxHtmlEditor, 
    DxToolbar, 
    DxItem, 
    DxSelectBox, 
    Lookup
}, 

  props:{
     
  }, 
  data(){ 
        return {
            id: String, 
        name: String, 
        type: String, 
        procedure: String, 
        url:String, 
        ingredients:Array, 
        ingredientSearch: String, 
        submitIngredient: String, 
        ingredient: '', 
        ingredientId:'', 
        quantity:'', 
        uom:'', 
        editRecipe: false, 
        addIngredient: false, 
        sizeValues: ['8pt', '10pt', '12pt', '14pt', '18pt', '24pt', '36pt'],
      fontValues: ['Arial', 'Courier New', 'Georgia', 'Impact', 'Lucida Console', 'Tahoma', 'Times New Roman', 'Verdana'],
      headerValues: [false, 1, 2, 3, 4, 5],
      isMultiline: true, 
      typeOptions: [{ID:1, Name: "Entry" }, {ID:2, Name: "Breakfast" }, {ID:3, Name: "Appitizer" }, {ID:4, Name: "Drinks" }]
       
       }
        
    }, 
    methods: {
         updateRecipe()
        {
            
            console.log(this.name, this.procedure, this.url); 
            var data = {
                name: this.name, 
                procedure: this.procedure, 
                type:this.type, 
                url: this.url, 
                id: this.id
                
            }
            fetch('https://zen-recipe.herokuapp.com/api/recipe/'+this.id , {
            method: 'POST', 
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(data) // body data type must match "Content-Type" header
        }).then(response =>{
            console.log(response); 
            this.editRecipe= false; 
        }).catch(err => {
            console.log(err); 
            alert("unable to uodate recipe: " + err); 
        })
        
        }, 
        editMode(){
            this.editRecipe = true; 
        }, 
        cancelEdit()
        {
            this.editRecipe= false; 
        }, 
        addIngredients()
        {
            this.addIngredient = true; 
        }, 
        cancelAdd()
        {
            this.addIngredient = false; 
        }, 
        searchIngredients(){
            console.log(this.ingredientSearch); 
        }, 
        getIngredientLookup(name, id){
            this.ingredient = name;
            this.ingredientId = id;  
            //console.log("Ingredient is: " + this.ingredient); 
        },
        async sendIngredient(){
            var data = {}; 
          data.recipe_id = this.id; 
          data.ingredient_id = this.ingredientId; 
          data.qty= this.quantity; 
          data.measure = this.uom; 
        
          console.log(data); 
           var resp =  await fetch('https://zen-recipe.herokuapp.com/api/recipe/ingredient/new/', {
            method: 'POST',
            headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
            },
            body: JSON.stringify(data)
        }); 
           var respData = await resp.json(); 
           console.log(respData); 
           fetch('https://zen-recipe.herokuapp.com/api/recipe/' + this.$route.params.id)
        .then(response => response.text())
        .then(data => {
            var res = JSON.parse(data); 
            res = res.recipe; 
            this.id=res.row_id; 
            this.name=res.name; 
            this.type=res.type; 
            this.procedure = res.procedure; 
            this.url = res.url; 
            this.ingredients = res.ingredients; 
            if(this.$route.query.edit  == "true")
            this.editRecipe = true; 
            this.addIngredient = false; 
        }).catch(err => console.log("error getting data >> ", err )); 
        
        }, 
        async deleteIngredient(ingredientId){
            console.log(url); 
            var url = 'https://zen-recipe.herokuapp.com/api/recipe/ingredient/' + ingredientId; 
            console.log(url); 
            var del = await fetch(url,  {
                method: 'DELETE'
            }); 
            var response = await del.json(); 
            console.log("response " + response); 
            if(response.msg == 'success'){
                this.ingredients = this.ingredients.filter(ingredient=> ingredient.recipe_ingredient_id != ingredientId)
            }
        }
    }, 
    mounted(){
        fetch('https://zen-recipe.herokuapp.com/api/recipe/' + this.$route.params.id)
        .then(response => response.text())
        .then(data => {
            var res = JSON.parse(data); 
            res = res.recipe; 
            this.id=res.row_id; 
            this.name=res.name; 
            this.type=res.type; 
            this.procedure = res.procedure; 
            this.url = res.url; 
            this.ingredients = res.ingredients.filter(ingredient => ingredient.ingredient_id != null); 
            if(this.$route.query.edit  == "true")
            this.editRecipe = true; 
            console.log('Ingredients' + this.ingredients); 
            
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
  
   background: #272626;
   
}


.container img{
  
    max-width:800px; 
    border: solid .5px #1f1e1e;
    border: .5px solid #1f1e1e;
    box-shadow: -0.5rem 0.5rem 2rem 0rem #0b0909; 
   margin-top:20px; 
}

ul{
      display: grid;
  grid-template-columns: 45% 5% 40% 10%;
   padding:0px 3rem; 
    gap: 10px; 


}

li{
    text-decoration: none;
    list-style: none;
    color:white; 
}
.section{
    display: flex;
    align-items: center;
    border-top: 1px grey solid;
     border-bottom: 1px grey solid;
}
.section span{
    text-align: right;
    flex-grow: 2;
    margin-right: 20px;
}
.section h2{
    margin:0px; 
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
    border-bottom: 1px solid grey;
}
.action-icon:hover{
 cursor: pointer;
}
input{
   
    height:30px; 
    font-size: 20px;
    border-radius: 5px;
    padding:10px 20px; 
    margin:20px 0px; 
}
select{
   width:100%; 
    height:35px; 
    font-size: 20px;
    border-radius: 5px;
    padding:0px 20px; 
    margin: 0px; 
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
    width:95%; 
}

.button{
    margin:15px; 
}
.actions{
    display:flex; 
}
.add-ing{
    margin:30px; 
}

.read-view img{
    height:400px; 
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

.recipe-type{
    
    display: flex;
    margin:40px; 
    gap:15px; 
    justify-content: right;
}
.recipe-type h4{
    margin: 0px; 
}



</style>
