<template>
    <div class="task-barr">
        <span class="text">{{percent}} %</span>
        <div class="progress-bar" :style="{width: percent + '%'}"></div>
    </div>
</template>

<script>
    export default{
        props:{
            percent: { type:Number, default: 0 }
        }
    }
</script>

<style>
  
    .task-barr { 
        position: relative;
        width: 80%;
        border-radius: 8px;
        border: 1px solid #fff;
        margin-bottom: 15px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .text{
        font-size: 1.5rem;
        /* display: flex;
        justify-content: center; */
        z-index: 1;
    }

    .progress-bar{
        position: absolute;
        align-self: flex-start;
        border-radius: 8px;
        background-color: #008000; 
        height: 100%;
    }
</style>