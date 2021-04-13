<template>
    <div class="container">
        <form v-on:submit="updateRecipe">
            <input type="text" name="name" id="name" v-model="name">
            <input type="text" name="procedure" id="procedure" v-model="procedure">
            <input type="text" name="url" id="url" v-model="url">
            <input type="text" name="id" id="id" v-model="id">
            <button type="submit">Save</button>
        </form>
    </div>
</template>

<script>
export default {
    props:{
       row_id: String 
    }, 
    data(){ 
        return {
            id: String, 
        name: String, 
        procedure: String, 
        url:String
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
        fetch('http://localhost:4000/api/recipe/' + this.row_id)
        .then(response => response.text())
        .then(data => {
            var res = JSON.parse(data); 
            res = res.recipe; 
            this.id=res.row_id; 
            this.name=res.name; 
            this.procedure = res.procedure; 
            this.url = res.url; 
        }).catch(err => console.log("error getting data >> ", err )); 
        
    }
}
</script>
<style scoped>

</style>