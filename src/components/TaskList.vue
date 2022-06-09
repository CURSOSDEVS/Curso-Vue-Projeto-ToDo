<template>
    <div class="task-list">
        <template v-if="tasks.length">
            <Task v-for="(task, i) in tasks" :key="task.name" :task="task"
                @deleteTask="deleteTask($event, i)"
                @changeStatusTask="$emit('changeStatusTask', i)"
            ></Task>
        </template>
        <p v-else class="no-task">Sua vida está em dia :)</p>
    </div>    
</template>

<script>
    import Task from './Task.vue'

    export default{
        components:{ Task},
        props:{
            tasks:{ type: Array, required: true}
        },
        methods: {
            deleteTask(task, i){
                this.$emit('deleteTask', i)
            }
        },
     }
</script>

<style>
    .task-list{
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }

    .task-list .task{
        margin: 10px;
    }

    .no-task{
        color: #ddd;
        font-size: 1.7rem;
    }
    
</style>

