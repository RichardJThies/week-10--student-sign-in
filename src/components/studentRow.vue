<template>
<tr v-bind:class="{present: student.present, absent: !student.present}"> <!--'student is a made up name for the students data property-->
    <td>{{student.name}}</td> <!--use dot notation to pull out specific parts of objects-->
    <td>{{student.starID}}</td> 
    <td>
        <input type="checkbox" v-bind:checked="student.present" v-on:change="arrivedOrLeft(student, $event.target.checked)"> <!--v-bind is 1 way data binding. v-on will call method if checkbox changes-->
    </td>
    <td v-show="edit"><img src="@/assets/delete.png" v-on:click="deleteStudent"></td><!--v-pn:click can be added to any element, not just buttons-->                                                                                       <!--^^$event.target is the html component(checkbox), .checked is boolean value-->
</tr>
</template>

<script>
export default {
    name: 'StudentRow',
    emits: ['student-arrived-or-left'], //document what what component does, what event it emits
    props: {
        student: Object,
        edit: Boolean //studentRow is being sent a v-bind instruction from parent on showing delete row & button for student rows
    },
    methods: {
        arrivedOrLeft(student, present){ //sends event to studentTable
            this.$emit('student-arrived-or-left', student, present)
        },
        deleteStudent(){//deleteStudent method itself cannot delete a student, must send event to studentTable which sends to App to delete student
            this.$emit('delete-student', this.student)
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