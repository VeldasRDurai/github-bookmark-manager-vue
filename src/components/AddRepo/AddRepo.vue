<script setup>
    import Wrapper from '../Wrapper/Wrapper.vue';
    import Search from '../Search/Search.vue';
    import ResultsTable from '../ResultTable/ResultTable.vue';

    import { reducer, initialState } from './reducer.js';
    import { searchRepos, searchUsers, getUserRepos } from "../../api";
</script>

<template>
    <Wrapper :heading="state.showUserRepos ? 'User repos' : 'Search'" >
        <div v-if="state.showUserRepos" >
            <b-button @click="dispatch({ type: 'reset.user.repos' })" >Go Back</b-button>
            <ResultsTable
                :dataHeaders="state.dataHeaders"
                :dataset="state.searchResults"
                :showButtonOption=true
                :buttonAction="index => handleRepositorySelect(index,this.state,this.dispatch)"
                :isLoading="state.isLoading"
                buttonText="Add"
                noRowsMessage="No search results" />
        </div>
        <div v-else >
            <Search
                :fieldValue="state.originalInput"
                :handleInputChage="handleInputChage"
                :handleSelectChange="handleSelectChange" />
                <div>
                    <ResultsTable v-if="state.typeInput === 'user'"
                        :dataHeaders="state.userDataHeaders"
                        :dataset="state.userSearchResults"
                        :showButtonOption=true
                        :buttonAction="index => handleUserSelect(index,this.state,this.dispatch)"
                        :isLoading="state.isLoading"
                        buttonText="View Repos"
                        noRowsMessage="No search results" />
                    <ResultsTable v-else
                        :dataHeaders="state.dataHeaders"
                        :dataset="state.searchResults"
                        :showButtonOption=true
                        :buttonAction="index => handleRepositorySelect(index,this.state,this.dispatch)"
                        :isLoading="state.isLoading"
                        buttonText="Add"
                        noRowsMessage="No search results" />
                </div>
        </div>
    </Wrapper>
</template>

<script>
    export default {
        props:[ 'addRepository' ],
        components:{ Search, Wrapper, ResultsTable },
        data(){
            return{
                state: initialState
            }
        },
        methods:{
            dispatch(action){ 
                this.state= reducer( this.state, action ) ;
            },
            fetchData: async (x,y) => {
                try {
                    if (x.searchInput === "") return;
                    y({ type: "set.loading", loading: true });
                    if (x.typeInput === "user") {
                        const response = await searchUsers(x.searchInput, x.pageNumber);
                        y({ type: "add.users", data: response });
                    } else {
                        const response = await searchRepos(x.searchInput, x.pageNumber);
                        y({ type: "add.repos", data: response });
                    }
                } catch (error) {
                    console.error(error);
                    y({ type: "set.loading", loading: false });
                }
            },
            handleInputChage(event){
                console.log( event );
                this.dispatch({ type: "updateinput", inputSearch: event });
                this.dispatch({ type: "search", search: event });
                this.fetchData( this.state, this.dispatch );
            },
            handleSelectChange(event){
                console.log( event );
                this.dispatch({ type: "update.type", typeInput: event });
                this.fetchData( this.state, this.dispatch );
            },
            handleRepositorySelect(index, x, y){
                this.addRepository(x.searchResults[index]);
                y({  type: "update.search.results", index });
            },
            handleUserSelect : async (index, x, y) => {
                try {
                    y({ type: "reset.user.repos", show: true, isLoading: true });
                    const response = await getUserRepos( x.userSearchResults[index].Repo.value );
                    console.log( response );
                    y({
                        type: "add.repos",
                        data: { items: response, total_count: response.length },
                        showUserRepos: true,
                    });
                } catch (error) {
                    console.error(error);
                    y({ type: "set.loading", loading: false });
                }
            },

        }
    }
</script>