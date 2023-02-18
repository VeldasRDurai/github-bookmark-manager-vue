<script>
	// import Navigation from "./components/navigation";
	// import Homepage from "./components/homepage";
	// import AddRepository from "./components/addrepo";
    import Navigation from "./components/Navigation/Navigation.vue";
	import ErrorWrapper from "./components/ErrorWrapper/ErrorWrapper.vue";
    import HomePage from "./components/HomePage/HomePage.vue";
    import AddRepository from './components/AddRepo/AddRepo.vue';
	export default {
        name: 'App',
		components:{ ErrorWrapper, 
            Navigation ,
            HomePage,
            AddRepository
        },
        data(){
            return {
                hasError: false,
                showAddPage:false,
                repositories:[],
            }
        },
        methods:{
            setHasError( value=true ){ this.hasError=value },
            setShowAddPage( value=true ){ this.showAddPage=value },
            addRepository(repos){ 
                this.repositories = [ repos,...this.repositories ]; 
                console.log( this.repositories );
            }
        }
    }
</script>
<template>
    <div>
        <ErrorWrapper  v-if="hasError" />
        <b-container v-else fluid class="p-5">
            <Navigation :showAddPage="showAddPage"
                @gotoHome="setShowAddPage(false)"
                @gotoAddNew="setShowAddPage()" />
            <div>
                <HomePage v-if="!showAddPage" :repositories="repositories" />
                <AddRepository v-else :addRepository="addRepository" />
            </div>
        </b-container>
    </div>
</template>


<style scoped>
</style>
