<template>
    <div class="task">
        <p>{{task.name}}</p>
    </div>
</template>

<script>
    export default{
        props:{
            task:{ type: Object, required: true}
        }
    }
</script>

<style>

</style>