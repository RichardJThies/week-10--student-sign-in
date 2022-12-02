<template>
    <div>
        <div class="alert alert-danger" v-if="errors.length > 0"> <!--Bootstrap alert-->
            <ul>
                <li v-for="error in errors">{{error}}</li> <!--loops over any error messages for display-->
            </ul>
        </div>

        <div class="card add-student m-2 p-2">
            <h4 class="card-title">Add new student</h4>

            <div class="form-group"> <!--bootsstrap classes-->
                <label for="name">Name</label>
   

                <input id="name" class="form-control" v-model.trim="newStudentName"> <!--Bootstrap classes-->
            </div>
            <div class="form-group"> 
                <label for="starID">Star ID</label>
    
                <input id="starID" class="form-control" v-model.trim="newStarID"> <!--.trim modifer converts any blank spaces from the beginning or ending of input, which will make the input invalid with validation-->
            </div>

            <button class="btn btn-primary" v-on:click="addStudent">Add</button> <!--v-on connects the button to the addStudent method-->
        </div>


    </div>
</template>

<script>
export default { // export default means another JS file can read whatever is inside. Whatever is read will be available to the reading file
    name: 'NewStudentForm', // common to give component same name as the file name
    emits: ['student-added'], //array documents events this component emits
    data() {
        return {
            newStudentName: '',
            newStarID: '',
            errors: []
        }
    },
    methods: {
        addStudent() { // this component does 1 job: be a form, display the form, validate it, then send an event to it's parent with data about new students
            this.errors = [] //clear errors array 

            if(!this.newStudentName){ //validation if no name
                this.errors.push('Must enter student name')
            }

            if(!this.newStarID) { //validation if no starID
                this.errors.push('Must enter starID')
            }

            if(this.errors.length == 0) {//if no errors in validation, input will be added to student array
                let student = {name: this.newStudentName, starID: this.newStarID, present: false} 
            
                // emit msg to parent with new student
                this.$emit('student-added', student)

                this.newStudentName = '' // clears the form after inputs because v-model uses 2 way data binding
                this.newStarID = ''

                
                }  
            }
        }
    }





</script>
<!----scoped means the styles will only apply to this component-->
<style scoped> 




</style>







