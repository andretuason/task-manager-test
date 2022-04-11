<template>
    <header>
        <h3>Task Tracker: </h3>
        <b-button @click="toggle" :pressed.sync="show" :variant="show ? 'danger' : 'success'">{{buttonText}}</b-button>
    </header>
</template>
<script>
export default {
    name: 'Header',
    data() {
        return {
            show: false,
            buttonText: 'Show'
        }
    },
    methods: {
        toggle(){            

            this.$emit('toggleDisplayAddTask')
            if (!this.show){
                this.buttonText = 'Show'
            }
            else{
                this.buttonText = 'Hide'
            }

        },

        
    }
}
</script>
<style scoped>

    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;

    }

</style>