<template>
    <div>
       <div v-for="item in items" :key="item.id">
            <list-item  :item="item" 
            class="item"
            v-on:itemChanged="$emit('reloadList')"
            />
       </div>
    </div>
</template>

<script>
import listItem from "./listItem.vue";
export default {
    name:'listView',
    components:{
        listItem,
    },
    props:{
        items: [],
    }
}
</script>

<style>
.item{
    background: floralwhite;
    padding: 5px;
    margin-top: 5px;
}
</style>
