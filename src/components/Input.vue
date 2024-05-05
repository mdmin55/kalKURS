<script>
export default{
    props:{
        changeAmount:{
            type: Function,
            required: true
        },
        convert:{
            type:Function,
            required:true
        },
      
    }
}
</script>

<template>
    <input min='0'type="number" @input="changeAmount($event.target.value)" placeholder="Введите число"><br>
    <button @click="convert()">Рассчитать</button>
</template>

<style scoped>
button{
    position:relative ;
    top: -10px;
    padding: 15px 15px;
    color:#fff;
    text-transform: uppercase;
    cursor: pointer;
    background-color: rgb(33, 21, 21);
    border-radius: 4px ;
    border: 0;
}
input{
    outline: none;
    border-radius: 3px;
    border: 0px;
    padding: 15px 20px;
    background:#ffffff;
    color: #333;
    width: 500px;
    top:-50px;
    font-size: 1.3em;
    position: relative;

}
button.fav-button{
    margin-left:20px;
}
</style>