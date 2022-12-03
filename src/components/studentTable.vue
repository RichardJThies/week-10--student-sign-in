<template>
    <div>
        <div class="card student-list m-2 p-2">
            <h4 class="card-title">Student List</h4>

            <div class="edit-table-toggle form-check">
                <input id="edit-table" type="checkbox" class="form-check-input" v-model="editTable">
                <label for="edit-table" class="form-check-label">Edit table?</label>
            </div>

            <div id="student-table">
                <table class="table">
                    <tr>
                        <th>Name</th>
                        <th>StarID</th>
                        <th>Present?</th>
                        <th v-show="editTable">Delete?</th>
                    </tr>

                    <student-row 
                        v-for='student in students'
                        v-bind:student="student" 
                        v-bind:key="student.starID"
                        v-bind:edit="editTable"
                        v-on:student-arrived-or-left="arrivedOrLeft"
                        v-on:delete-student="deleteStudent">
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
    data() {
        return {
            editTable: false
        }
    },
    methods: {//not best pratice to have methods of the same name as methods in child components when sending events upward. It's confusing?
        arrivedOrLeft(student, present) {//emit msg/event to parent, when the checkbox is checked or unchecked.
            this.$emit('student-arrived-or-left', student, present)//1st argument is sending the student object, containing name & starID. Present contains new value of whether they are present or not.
        },
        deleteStudent(student) {
            this.$emit('delete-student', student)
        }
    }
}
</script>

<style scoped> /*scoped means the styles will only apply to this component*/

</style>