<template>
    <div class="item">
        <input type="checkbox" @change="updateCheck()"  v-model="item.completed"/>
        <span :class="[item.completed ? 'completed' : '', 'itemText']">{{item.name}}</span>
        <button v-on:click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash"/>
        </button>
    </div>
</template>

<script>
export default {
    name: 'listItem',
    props:{
        item :[]
    },
    data(){
        return{
            check: false,
        }
    },
    methods:{
        updateCheck(){
            axios.put('api/item/'+this.item.id, {
                item : this.item
            }).then(response =>{
                if(response.status == 200){
                    this.$emit('itemChanged');
                }
            }).catch(error =>{
                console.log(erroe);
            })
        },
        removeItem(){
            axios.delete('api/item/' + this.item.id).then(response => {
                if(response.status == 200){
                    this.$emit('itemChanged');
                }
            }).catch(error => {
                console.log(error);
            })
        }
    }
}
</script>

<style>
.completed{
    text-decoration: line-through;
    color: darkgray;
}
.itemText{
    width: 100%;
    margin-left: 20px;
}
.item{
    display: flex;
    justify-content: center;
    align-items: center;
 }
 .trashcan{
    background: #e6e6e6e6;
    color: red;
    border: none;
    outline: none;
 }
</style>
