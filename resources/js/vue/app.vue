<template lang="">
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <addItemForm v-on:reloadList="getList()" />
        </div>
        <listView 
            :items="items"
            v-on:reloadList="getList()"
        />
    </div>
</template>

<script>
import addItemForm from './addItemForm'
import listView from './listView'
export default {
    data: function(){
        return{
            items: []
        }
    },
    components:{
        addItemForm,
        listView
    },
    methods: {
        getList(){
            axios.get('api/items')
            .then(response =>{
                this.items = response.data
            })
            .catch(error =>{
                console.log(error);
            })
        }
    },
    created() {
        this.getList();
    },
}
</script>

<style scoped>
    .todoListContainer{
        width: 500px;
        margin: auto;
        margin-top: 10px;
    }

    .heading{
        background: #e6e6e6;
        padding: 10px;
    }

    #title{
        text-align: center;
    }
</style>