<template>
    <div>
        <div v-if="student.name"> <!--is something in the object? If not, then do nothing-->
            <div class="alert alert-success" v-if="student.present"> <!--if the checkbox is checked, display message.-->
                Welcome, {{student.name}}.
            </div>

            <div class="alert alert-info" v-else> <!--since the checkbox is true or false, use v-else to display messsage if false.-->
                Goodbye, {{student.name}}, see you later.
            </div>
        </div>


    </div>
</template>

<script>
export default { // export default means another JS file can read whatever is inside. Whatever is read will be available to the reading file
    name: 'StudentMessage', //studentMessage will be sent a student to display a message for by App.vue
    props: {
        student: Object // data class, not a value
    }
}




</script>
<!----scoped means the styles will only apply to this component-->
<style scoped> 




</style>







