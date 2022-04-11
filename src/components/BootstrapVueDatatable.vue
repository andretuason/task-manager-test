<template>
    <div>
        <b-table striped hover  primary-key="id" :items="posts"></b-table>
        <!-- <b-table striped hover :fields="fields" :items="posts"></b-table> -->
    </div>
</template>

<script>
export default {
 name: 'BootstrapVueDatatable',
    props:{
        // fields: ['Task Name', 'Duration in Hours', 'Status', 'Start Date', 'End Date', 'People Working on Task', 'Notes'],
        posts: [],


    },
    data(){
        return {
        }
    }

    
}
</script>