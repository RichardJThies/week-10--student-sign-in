<template>
  <div id="app">
    <new-student-form v-on:student-added="newStudentAdded"></new-student-form><!--App.vue receives event from newStudentForm, calls method-->
    <student-table 
    v-bind:students="students" 
    v-on:student-arrived-or-left="studentArrivedOrLeft"
    v-on:delete-student="deleteStudent"></student-table><!--App.vue sends student array to studentTable prop. Reveives event back with new data after input. Receives event to delete student-->
    <student-message v-bind:student="mostRecentStudent"></student-message><!--App.vue will send studentMessage data for it's prop-->
  </div>
</template>

<script>
import NewStudentForm from './components/newStudentForm.vue';
import StudentMessage from './components/studentMessage.vue';
import StudentTable from './components/studentTable.vue';

export default {
  name: 'App',
  components: {// lets App know it has child components
    NewStudentForm,
    StudentMessage,
    StudentTable
  },
  data() { // function returns object
    return {
      students: [], // list of students received from newStudentForrm
      mostRecentStudent: {}
    }
  },
  methods: {
    newStudentAdded(student) { //method recieves event from newStudentForm, puts student object into array
      this.students.push(student)
      this.students.sort(function(s1, s2) {
        return s1.name.toLowerCase() < s2.name.toLowerCase() ? -1 : 1// sorts the students in name order
      })
    },
    studentArrivedOrLeft(student, present) { // student & present arguments arrive from event sent by studentTable
      //find student in array of students, update present attribute
      let updateStudent = this.students.find(function(s) {//.find is a JS method that returns a matching element in an array. The method contains a function.
        if(s.name === student.name && s.starID === student.starID) {//function must return true value for element that it is searching for, will be called for every element in array
          return true // if the name & starID match, the function will return true
        }
      })

      if (updateStudent) {//if a student is found, the present received from studentTable is assigned
        updateStudent.present = present
        this.mostRecentStudent = updateStudent//make sure mostRecentStudent is assign its namesake
      }
    },
    deleteStudent(student) {
      this.students = this.students.filter(function(s) {//.filter takes a function as an argument. It checks every student in student array, if they match a condition, they stay. If not, they are removed
        if(s != student) {//filter returns new array when the function returns true
          return true //undefined is treated as false
        }
      })
    }
  }
}
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/bootstrap@4.6.0/dist/css/bootstrap.min.css"; /*App.vue is the parent component and the page itself. Therefore bootstrap will be applied to all components*/
</style>