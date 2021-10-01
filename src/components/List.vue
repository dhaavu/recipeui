<template>
     <div class="card-container">
            <div v-for="(item) in items" :key="item.row_id" class="card">
                <div class="card-body">
                <router-link :to="{path: '/recipe/' + item.row_id}">
                    <img :src="item.url" />
                </router-link>
                <h2>{{item.name}}</h2>
               <!-- {{item.procedure.substring(0,100)}} -->
                <p class="desc" v-html="item.procedure.substring(0,100)"> </p>
                 <h4>{{item.type}}</h4>
            </div>
            <div class="card-action">
                <router-link class="brand-link" :to=" {path:`/recipe/${item.row_id}`, query: {edit: 'true'} }">
                 <span class="material-icons">
                    edit
                </span>
                </router-link>
               
                <span class="material-icons">
                    delete
                </span>

            </div>
        </div>
     </div>
</template>

<script>
export default {
    name: 'List', 
    props:{
        items: Array
    },
   
    methods: {

    }
}
</script>

<style scoped>

.card-container{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: center;  
}

.card{
    background:#1f1e1e; 
    order:4;
    margin:20px;  
    width:300px; 
    border-radius: 20px;
    border: .5px solid #1f1e1e;
    box-shadow: -0.5rem 0.5rem 2rem 0rem #0b0909
}

.card img{
    width:300px; 
    height:300px;
    border: solid .5px #1f1e1e;
    border-radius: 20px 20px 0px 0px;
}

.card-action{
    display: flex;
    justify-content: center;
    padding: 20px;
    gap: 3rem;
    border-top: 3px solid #4c4b4b;
    font-size: 28px;
}

.card-action span{
    font-size: 28px;
}



.desc{
    height:90px; 
    font-size:18px; 
}

</style>
