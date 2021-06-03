<template>
  <div id="app">
    <b-container>
      <b-table :items="allStudent" striped hover></b-table>
    </b-container>

    <b-container>
      <b-table :items="allCourse" striped hover></b-table>
    </b-container>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  components: {
  },

  data(){
    return{
      allStudent: [],
      msg: '',

      allCourse: [],
      msg2: '',
    }
  },

  methods:{
    async callAllAPIs(){
      await Promise.all([
        this.getAllStudents(),this.getAllCourses()
      ])
    },

    async getAllStudents(){
      try{
        const x = await axios.get('http://sun.beyond.photos:5000/student')

        if(x.data.data.length>0){
          this.allStudent= x.data.data
        }

        else{
          this.msg= x.data.msg
        }
      }

      catch(err){
        console.log(err.message)
      }
    },

    async getAllCourses(){
      try{
        const x = await axios.get('http://localhost:5000/courses')

        if(x.data.length>0){
          this.allCourse= x.data
        }

        else{
          this.msg2= x.data.msg
        }
      }

      catch(err){
        console.log(err.message)
      }
    }
  },

  mounted(){
    this.callAllAPIs()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
