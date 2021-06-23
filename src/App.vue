<template>

  
    <Header  heading="Tasker"/>
    <AddTask @add-task="addTask"/>
    <TasksContainer @remind="remind"   @deleteTask="deleteTask"   :tasks="this.tasks"/>
   
  
  
</template>

<script>
import Header from "./components/Header"
import TasksContainer from "./components/TasksContainer"
import AddTask from "./components/AddTask"

export default {
  name: 'App',
  components:{
    Header,TasksContainer,AddTask
  },
data(){
  return {
    tasks:[]
  }
},

 methods:{
            async deleteTask(id){

              
               let res = await fetch(`http://localhost:5000/tasks/${id}`,{
                  method:'DELETE',
               
                })

             

                if(res.status===200){

                  this.tasks= this.tasks.filter((arr)=>{
                  return arr.id!==id
                  })
                  
                  }
                 else {
                  alert("Error Deleting!!")
                }

            },









            async remind(id){
              
              let fetchedTask = await this.fetchApiId(id)
                     
                     console.log(fetchedTask.reminder)
                     fetchedTask.reminder=!fetchedTask.reminder

                const res = await fetch(`http://localhost:5000/tasks/${id}`, {
                method: 'PUT',
                headers: {
                  'Content-type': 'application/json',
                },
                body: JSON.stringify(fetchedTask),
              })
      
              let data = await res.json()

              console.log(data)
                this.tasks.map((arrEl)=>{
                  if(arrEl.id==id){
                    arrEl.reminder=data.reminder
                  }
                })

            

                
            },
            async addTask(newTask){

              


              let res = await fetch(`http://localhost:5000/tasks`,{
                method:'POST',
                 headers: {
                  'Content-type': 'application/json',
                },
                body: JSON.stringify(newTask),
              })

              console.log(res)

              let data = await res.json()

              console.log(data)

              this.tasks= [
                ...this.tasks,
                  data
              ]
              // console.log(newTask)
              },

              async fetchApi(){
                
                let res = await fetch(`http://localhost:5000/tasks`)
                let data = await res.json()

                return data
              },
            
            async fetchApiId(id){
              let res = await fetch(`http://localhost:5000/tasks/${id}`)
                let data = await res.json()

                return data
            }

  },
  
 async created(){
  // this.fetchApi().then((result)=>{this.tasks=result})

  let fetchedTasks = await this.fetchApi()
  this.tasks = fetchedTasks
 
}


}



</script>

<style>
body{
  margin:0;
  padding:0;
}


#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #3d405b;
  
  display:flex;
  flex-direction: column;
  background-color:#f4f1de;
  min-height: 100vh;
  
 
  align-items: center;
}
</style>
