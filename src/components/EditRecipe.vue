<template>
    <div>
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
</template>
<script>
import Button from "../components/button.vue"; 
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
    DxSelectBox
}, 
    props:{
             id: String, 
        name: String, 
        type: String, 
        procedure: String, 
        url:String, 
        ingredients:Array, 
       
    }, 
    data(){ 
    return{
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
        
        } 
    },
}
</script>