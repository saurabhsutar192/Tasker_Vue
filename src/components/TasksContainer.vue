<template>

    <div  :key="task.id" v-for="task in tasks"  >
        <Tasks  @remind="$emit('remind',task.id)"  @deleteTask="$emit('deleteTask',task.id)" :task="task"/>
        
    </div>

    
</template>





<script>

import Tasks from "./Tasks"

export default {
    name:'TasksContainer',
    components:{
        Tasks
    },
    props:{
        tasks:Array
        },
        emits:['deleteTask','remind']
}
</script>