<template>
    <!-- <div class="container">
        <ul class="list">
        <li v-for="(item, index) in items" :key="index">
           <div class="picture">
               <img v-bind:src="item.url" alt="Recipe Image" srcset="">
           </div>
            <div class="title">
                <h3>{{item.title}}</h3>
                <p>{{item.description}}</p>
            </div>
            <div class="action">
                <a class="material-icons">arrow_forward_ios </a>
         
            </div>
          </li>
    </ul>
    </div> -->

    <div class="card-container">
            <div class="card">
                <div class="card-body">
                <img src="https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg" />
                <h3>Title</h3>
                <p>Description .......</p>
            </div>
            <div class="card-action">
                <span class="material-icons">
                    edit
                </span>
                <span class="material-icons">
                    delete-outline
                </span>

            </div>
        </div>

          <div class="card">
                <div class="card-body">
                <img src="https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg" />
                <h3>Title</h3>
                <p>Description .......</p>
            </div>
            <div class="card-action">
                <span class="material-icons">
                    edit
                </span>
                <span class="material-icons">
                    delete-outline
                </span>

            </div>
        </div>

          <div class="card" style="background-size:cover; background:url('https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg')">
                <div class="card-body">
                <img src="" />
                <h3>Title</h3>
                <p>Description .......</p>
            </div>
            <div class="card-action">
                <span class="material-icons">
                    edit
                </span>
                <span class="material-icons">
                    delete-outline
                </span>

            </div>
        </div>

          <div class="card">
                <div class="card-body">
                <img src="https://www.cookwithmanali.com/wp-content/uploads/2020/05/Masala-Dosa.jpg" />
                <h3>Title</h3>
                <p>Description .......</p>
            </div>
            <div class="card-action">
                <span class="material-icons">
                    edit
                </span>
                <span class="material-icons">
                    delete-outline
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
    background:#42b983; 
    order:4;
    margin:20px;  
    width:300px; 
}

img{width:300px; 
height:300px}




li{
    display: grid;
   grid-template-columns: auto auto auto;
    grid-gap: 10px;
    padding: 5px;
    border:1px solid rgb(218, 215, 215); 
    margin:5px; 
    box-shadow: 0 8px 6px 0px rgb(211, 211, 211);
    
}
 ul{
     padding:0px; 
     margin:20px;
     
 }

/* img{
    width:85px; 
    height: 85px;
    border-radius:5px;
} */

.picture {
  display: flex;
  align-items: center;
  justify-content: center;
}

.action {
  display: flex;
  align-items: center;
  justify-content: center;
}
.title {
  text-align: left;
  
}
.container{
    max-width: 800px;
    margin:0 auto; 
}
</style>
