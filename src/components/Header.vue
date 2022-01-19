<template>
   <section class="container">
       <h1>BOOLFLIX</h1>
        <div class="search">
            <input v-model="userResearch" type="text"/>
            <button @click="$emit('search', userResearch)">Search</button>
        </div>
   </section>
</template>

<script>
export default {
    name: 'Header',
    data: function(){
        return {
            userResearch: ''
        }
    }
}
</script>

<style lang="scss" scoped>
@import '../style/common.scss';

    section{
        height: 100px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        
        h1{
            color: red;
            font-weight: 800;
        }

        input{
            margin: 0 20px;
            border-radius: 10px;
            border: 1px solid red;
            padding: 2px 15px;
            line-height: 25px;
        }

        button{
            padding: 5px 10px;
            border: 1px solid red;
            border-radius: 10px;
            background-color: white;
            cursor: pointer;
        }
    }
</style>