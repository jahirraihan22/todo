<template>
    <div class="addItem">
        <input type="text" v-model="item.name"/>
        <font-awesome-icon 
            icon="plus-square"
            :class="[ item.name ? 'active' : 'inactive', 'plus' ]"
            @click="addItem()"
        />
    </div>
</template>
<script>
export default {
    data: function (){
        return {
            item: {
                name: ""
            }
        }
    },
    methods: {
        addItem(){
            if(this.item.name == ""){
                return;
            }
            axios.post('api/item/store',{
                name: this.item.name
            })
            .then(response => {
                if(response.status == 201){
                    this.item.name = "";
                    this.$emit('reloadList');
                }
            })
            .catch(error =>{
                console.log(error);
            })
        }
    }
    
}
</script>
<style scoped>
    .addItem{
        display: flex;
        justify-content:center;
        align-items:center;
   }
   input{
       background: #f7f7f7;
       border: 0px;
       outline: none;
       padding: 5px;
       margin-right: 10px;
       width: 100%;
   }   
   .plus{
       font-size:20px;
       cursor: pointer;
   } 
   .active{
       color: #00CE25;
   }
   .inactive{
       color: #999999;
   }
</style>
