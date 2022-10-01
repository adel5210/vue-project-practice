<script>
    export default{
        props:{
            msg: String
        },
        emits:['response'],
        created(){
            this.$emit('response',"Hello from child");
        }
    }
</script>
<template>
    <h2>{{ msg || 'No data' }}</h2>
    
</template>