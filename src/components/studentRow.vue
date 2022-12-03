<template>
<tr v-bind:class="{present: student.present, absent: !student.present}"> <!--'student is a made up name for the students data property-->
    <td>{{student.name}}</td> <!--use dot notation to pull out specific parts of objects-->
    <td>{{student.starID}}</td> 
    <td>
        <input type="checkbox" v-bind:checked="student.present" v-on:change="arrivedOrLeft(student, $event.target.checked)"> <!--v-bind is 1 way data binding. v-on will call method if checkbox changes-->
    </td>                                                                                       <!--^^$event.target is the html component(checkbox), .checked is boolean value-->
</tr>
</template>

<script>
export default {
    name: 'StudentRow',
    props: {
        student: Object
    },
    methods: {
        arrivedOrLeft(student, present){ //sends event to studentTable
        this.$emit('student-arrived-or-left', student, present)
        }
    }
}


</script>


<style scoped>
.present {
    color: gray;
    font-style: italic;
    background-color: aliceblue;
}

.absent {
    color: black;
    font-weight: bold;
    background-color: bisque;
}




</style>