<template>
    <div class="container">
        <b-table striped hover primary-key="id" :fields="fields" :items="posts"></b-table>
        <!-- <b-table striped hover :fields="fields" :items="posts"></b-table> -->
    </div>
</template>

<script>
export default {
 name: 'BootstrapVueDatatable',
    props:{
        posts: [],


    },
    data(){
        return {
            fields: ['taskName', 'durationHours', 'status', 'startDate', 'endDate', 'notes', 'delete'],
        }
    },
    methods: {
       deleteRow(index){
           posts.deleteRow(index)
       }
    }

    
}
</script>

<style scoped>

*{
    margin-bottom: 500px;
}
</style>
