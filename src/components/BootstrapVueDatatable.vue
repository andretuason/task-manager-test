<template>
    <div class="container pt-3 pb-5">
        <h2>BootstrapVue datatable</h2>
        <b-table striped hover  primary-key="id" :items="posts"></b-table>
        <!-- <b-table striped hover :fields="fields" :items="posts"></b-table> -->
    </div>
</template>

<script>
export default {

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