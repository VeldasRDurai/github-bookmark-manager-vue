<template>
    <b-table-simple striped bordered hover class="mt-3">
        <b-thead>
            <b-tr>
                <b-th v-for="header,key in dataHeaders" :key="key" >{{ header }}</b-th>
                <span>
                    <b-th v-if="showButtonOption"></b-th>
                </span>
            </b-tr>
        </b-thead>
        <b-tbody>
            <b-tr v-if="isLoading || ( dataset && dataset.length === 0) " >
                <b-td class="no-rows-message" colspan="6">
                    {{ isLoading ? "Loading..." : noRowsMessage }}
                </b-td>
            </b-tr>
            <b-tr v-else v-for="(data, index) in dataset">
                <b-td key="index" v-for="(header, innerIndex) in dataHeaders" >
                    <b-td key="innerIndex" >
                        <span v-if="header === 'Index'" > {{ index + 1 }} </span>
                        <a v-else-if="data[header].isLink" :href="data['URL'].value" target="_blank" rel="noopener noreferrer">
                            {{ data[header].value }}
                        </a>
                        <span v-else> {{ data[header].value }} </span>
                    </b-td>
                </b-td>
                <b-td v-if="showButtonOption" >
                    <b-button @click="buttonAction(index)" >
                        {{buttonText}}
                    </b-button>
                </b-td>
            </b-tr>
        </b-tbody>
    </b-table-simple>
</template>

<script>
    export default {
        props:[ 'dataHeaders', 'showButtonOption', "isLoading", "dataset", "noRowsMessage", "buttonText", "buttonAction" ],
        methods:{
            mounted(){
                console.log({ dataHeaders, showButtonOption, isLoading, dataset, noRowsMessage, buttonText, buttonAction });
            }
        }
    }
</script>

<style>
    .no-rows-message {
        text-align: center;
    }
</style>