<template>
    <div class="container">
        <b-table striped hover primary-key="id" :fields="fields" :filter="filter" :items="posts">
            <template v-slot:cell(delete)="data">
                <i class="fa-solid fa-xmark" @click="deleteRow(data.item.id)"></i>
            </template>

        </b-table>
        <!-- <b-table striped hover :fields="fields" :items="posts"></b-table> -->
    </div>
</template>

<script>
export default {
 name: 'BootstrapVueDatatable',
    props:{
        posts: [],
        filter: ""
        
    },
    data(){
        return {
            fields: ['taskName', 'durationHours', 'status', 'startDate', 'endDate', 'notes', 'delete'],
            
        }
    },
    methods: {
       deleteRow(id){
           if (confirm("Are you sure you want to delete row?")){
            const index = this.posts.indexOf((x) => x.id === id);
            this.$emit('delete-task', id)
           }
            console.log(id)
           
       }
    }

    
}
</script>

<style scoped>
.fa-solid.fa-xmark{
    color: red;
}

</style>
