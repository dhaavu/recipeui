<template>
    <span :style="{background:backgroundColor}">{{buttonText}}</span>
</template>
<script>
export default {
    props:{
        buttonText:String,  
        backgroundColor: String
    }
}
</script>
<style scoped>
span{
   
    color:white; 
    padding:10px 40px;
     
  
    display: block;
    font-size: 20px;
    
}

span:hover{
    cursor: pointer;
}
</style>