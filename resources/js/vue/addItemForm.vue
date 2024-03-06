<template>
    <div class="addItem">
        <input type="text" v-model="item.name"/>
        <font-awesome-icon icon="plus-square"
                           :class="[item.name ? 'active' : 'inactive', 'plus']"
                           v-on:click="addItem"
        />
    </div>
</template>

<script>
export default {
    name : 'addItemForm',
    data(){
        return {
            item :{
                name: "",
            }
        }
    },
    methods:{
        addItem(){
            if(this.item.name == ''){
                return;
            }
            axios.post('api/item/store', {
                item : this.item
            }).then( response => {
                if(response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadList');
                }
            }).catch(error =>{
                console.log(error);
            })
        }
    }
}
</script>

<style>
.addItem{
    display: flex;
    justify-content: center;
    align-items:center;
}
input{
    background: ivory;
    border: 0;
    outline : none;
    padding:5px;
    margin-right:10px;
    width:100%;
}
.plus{
    font-size: 20px;
}
.active{
    color: green;
}
.inactive{
    color: darkgray;
}
</style>
