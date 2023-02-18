<template>
    <b-form inline class="justify-content-center" >
        <div class="search-heading">Search Options:</div>
        <b-form-group label="Type:" label-for="type-select" >
            <b-form-select id="type-select" class="ml-4 mr-1" 
                @change="handleSelectChange($event)" >
                <b-form-select-option value="user">Users</b-form-select-option>
                <b-form-select-option value="repo">Repository</b-form-select-option>
            </b-form-select>
        </b-form-group>

        <b-form-group label="Search:" label-for="type-select" >
            <b-form-input id="search-box" className="ml-4 mr-1"
                placeholder="Enter text to search"
                @change="handleInputChage($event)" />
        </b-form-group>
    </b-form>
</template>

<script>
    export default {
        props:[ 'fieldValue', 'handleInputChage', 'handleSelectChange' ]
    }
</script>