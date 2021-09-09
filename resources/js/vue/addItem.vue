<template>
<div class="inputFiled">
<input type="text" v-model="item.name"/>
<font-awesome-icon icon="plus-square"
@click="addItem()"
:class="[ item.name ? 'active' : 'inactive','plus']"/>
 </div>
</template>
<script>
    export default {
        data: function() {
            return {
                item: {
                    name: ""
                }
            }

        },
        methods: {
            addItem(){
            if(this.item.name==''){
                return window.alert("Please enter a task name");
                
            }
            axios.post('api/item/store',{
                item: this.item
                
            })
            .then( response => {
                if(response.status==201){
                    this.item.name = "";
                    this.$emit('reloadList');
                }
            })
            .catch(error => {
                console.log(error);
            })
        }


    }
    }
</script>
<style scoped>
    .inputFiled {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
    input {
        background: white;
        border: 0px;
        outline: none;
        width: 100%;
        padding: 5px;
        margin-right: 10px;
    }
    
    .plus {
        font-size: 20px;
    }
    
    .active {
        color: #0eff42;
    }
    
    .inactive {
        color: #5e5e6e;
    }
</style>
