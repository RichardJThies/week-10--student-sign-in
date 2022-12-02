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

                    <tr v-for='student in students' v-bind:key="student.starID" v-bind:class="{present: student.present, absent: !student.present}"> <!--'student is a made up name for the students data property
                                                                                  ^^ v-bind sets html attributes on elements like classes'-->
                        <td>{{student.name}}</td> <!--use dot notation to pull out specific parts of objects-->
                        <td>{{student.starID}}</td> 
                        <td>
                            <input type="checkbox" v-bind:checked="student.present" v-on:change="arrivedOrLeft(student, $event.target.checked)"> <!--v-bind is 1 way data binding. v-on will call method if checkbox changes-->
                        </td>                                                                                       <!--^^$event.target is the html component(checkbox), .checked is boolean value-->
                    </tr>
                </table>
            </div>
        </div>


    </div>
</template>

<script>
export default { // export default means another JS file can read whatever is inside. Whatever is read will be available to the reading file
    name: 'StudentTable', // studentTable is given a list of students to draw/display in the table. App.vue will manage array of students which it will provide to studentTable
    emits: ['student-arrived-or-left'], //document what what component does, what event it emits
    props: {
        students: Array // Array is a data type, not value
    },
    methods: {
        arrivedOrLeft(student, present) {//emit msg/event to parent, when the checkbox is checked or unchecked.
            this.$emit('student-arrived-or-left', student, present)//1st argument is sending the student object, containing name & starID. Present contains new value of whether they are present or not.
        }
    }
}




</script>

<style scoped> /*scoped means the styles will only apply to this component*/
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







