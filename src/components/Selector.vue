<script>
export default{
    props:{
        setKurs:{
        type:Function,
        required:true}
    }, 
    data(){
        return{
            current: ''
        }},
    methods:{
        selectItem(val){
            this.setKurs(val);
            this.current = val;

        }
}}
</script>

<template>
    <ui>
        <li @click="selectItem('RUB')":className="current == 'RUB' ? 'active': ''">RUB</li>
        <li @click="selectItem('USD')":className="current == 'USD' ? 'active': ''">USD</li> 
        <li @click="selectItem('EUR')":className="current == 'EUR' ? 'active': ''">EUR</li>
        <li @click="selectItem('KRW')":className="current == 'KRW' ? 'active': ''">KRW</li>
    </ui>
</template>

<style scoped>
ui{
  padding: 0px;
    width: 150px;
    list-style: none;
    color:azure;
    border-radius: 3px;
}
li{
    display: block;
    padding: 10px 0;
    background: #261f1f;
}
li:hover, li.active{
background: #35315b;
cursor: pointer;
}
</style>