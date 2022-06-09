<template>
    <div @click="$emit('changeStatusTask', task)" class="task" :class="stateClass">
        <span @click.stop="deleteTask" class="close">x</span>
        <p>{{task.name}}</p>
    </div>
</template>

<script>
    export default{
        props:{
            task:{ type: Object, required: true}
        },
       computed:{
           stateClass(){
               return{
                   pending: this.task.pending,
                   done: !this.task.pending
               }
           }
       },
       methods: {
           deleteTask(){
               this.$emit('deleteTask', this.task)
           }
       },
    }
</script>

<style>
    .task{
        position: relative;
        box-sizing: border-box;
        width: 350px;
        height: 150px;
        padding: 10px;
        border-radius: 8px;
        font-size: 2rem;
        font-weight: 300;
        cursor: pointer;
        user-select: none;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .pending{
        border-left: 12px solid #8B0000;
        background-color: #b22222;
    }

    .done{
        color: #ddd;
        text-decoration: line-through;
        border-left: 12px solid #006400;
        background-color: #008000;
    }

   .pending .close{
       background-color: #8B0000;
   }

   .done .close{
       background-color: #006400;;
   }

   .close{
       position: absolute;
       right: 10px;
       top: 10px;
       font-size: 0.9rem;
       font-weight: 600;
       height: 20px;
       width: 20px;
       border-radius: 10px;
       display: flex;
       justify-content: center;
   }
</style>