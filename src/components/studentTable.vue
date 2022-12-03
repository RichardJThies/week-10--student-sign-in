<template>
    <div>
        <div class="card student-list m-2 p-2">
            <h4 class="card-title">Student List</h4>
            <div id="student-table">
                <table class="table">
                    <tr>
                        <th>Name</th>
                        <th>StarID</th>
                        <th>Present?</th>
                    </tr>

                    <student-row 
                        v-for='student in students'
                        v-bind:student="student" 
                        v-bind:key="student.starID"
                        v-on:student-arrived-or-left="arrivedOrLeft">
                    </student-row> <!--student row creates new studentRow components?-->
                </table>
            </div>
        </div>


    </div>
</template>

<script>
import StudentRow from "@/components/studentRow.vue"
export default { // export default means another JS file can read whatever is inside. Whatever is read will be available to the reading file
    name: 'StudentTable', // studentTable is given a list of students to draw/display in the table. App.vue will manage array of students which it will provide to studentTable
    components: {// lets studentTable know it has a child component
        StudentRow
    },
    emits: ['student-arrived-or-left'], //document what what component does, what event it emits
    props: {
        students: Array // Array is a data type, not value
    },
    methods: {//not best pratice to have methods of the same name when sending events upward, confusing?
        arrivedOrLeft(student, present) {//emit msg/event to parent, when the checkbox is checked or unchecked.
            this.$emit('student-arrived-or-left', student, present)//1st argument is sending the student object, containing name & starID. Present contains new value of whether they are present or not.
        }
    }
}




</script>

<style scoped> /*scoped means the styles will only apply to this component*/

</style>







