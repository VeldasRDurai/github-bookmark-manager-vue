<script setup>
    import Wrapper from '../Wrapper/Wrapper.vue';
    import ResultTable from '../ResultTable/ResultTable.vue';
</script>

<template>
    <Wrapper heading="Home">
        <ResultTable :dataHeaders="dataHeaders"
            noRowsMessage="No repos added yet" 
            :showButtonOption=false 
            :isLoading=false
            :dataset=repositories 
            buttonText="" 
            :buttonAction="undefined"
            />
    </Wrapper>
</template>

<script>
    export default {
        data(){
            return {
                dataHeaders:["Index", "Name", "Maintainer", "Created", "URL"],
            }
        },
        props:[ 'repositories' ]
    }
</script>
