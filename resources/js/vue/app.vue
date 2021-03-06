<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="tittle">Todo List</h2>
            <add-item-from 
                v-on:reloadList="getItemList()"
            />
        </div>
        <list-view 
            :items="items"
            v-on:reloadList="getItemList()"
        />
    </div>
</template>
<script>
import addItemFrom from "./addItemForm.vue";
import listView from "./listView.vue";

export default {
    components: {
        addItemFrom,
        listView
    },
    data : function (){
        return {
            items: []
        }
    },
    methods : {
        getItemList () {
            axios.get('api/items')
            .then( response => {
                this.items = response.data;
            })
            .catch(error => {
                console.log(error);
            })
        }
    },
    created () {
        this.getItemList();
    }
}
</script>
<style scoped>
    .todoListContainer {
        width: 350px;
        height: auto;
        margin: auto;
    }
    .heading {
        background: #e6e6e6;
        padding: 10px;
    }
    #tittle {
        text-align: center;
    }
</style>