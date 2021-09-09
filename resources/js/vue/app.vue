<template>

    <div class="container">
        <div class="heading">
               <h1 id='title'>My to do list App</h1>
               <add-item
               v-on:reloadList="$emit(returnDb())" />
        </div>
         <list-View :items="items" 
         v-on:reloadList="returnDb()"/>  
        </div>
</template>
<script>
    import addItem from "./addItem"
    import listView from "./listView"
    export default {
        components: {
            addItem,
            listView

        },
        data:function (){
            return{
                items:[]
            }
        },
        methods: {
            returnDb(){
                axios.get('api/items')
                .then(response=>{
                    this.items = response.data
                })
                .catch(error =>{
                    console.error(error);
                })
            }
        },
        created(){
            this.returnDb();
        }

    }
</script>
<style scoped>
    .container {
        width: 400px;
        margin: auto;
    }
    
    .heading {
        background: #e6e6e6;
        padding: 10px;
        text-align: center;
        font-family: Cabril;
    }
    
    .title {
        font-size: 80px;
    }
</style>