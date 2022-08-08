<template>
    <div class="app">
        <div class="app-content">

            <my-modal
            v-model:show="addCompanyModalShow"
            >

                <create-company
                v-model:show="addCompanyModalShow"
                @create="createCompany"
                />

            </my-modal>

            <div class="action-content">
                <my-input
                placeholder="Найти по ФИО..."
                v-model.trim="searchValue"
                @input="pagination.currentPage = 0"
                />

                <my-button
                @click="addCompanyModalShow = true"
                >Добавить</my-button>
            </div>

            <table class="table">
                <table-head
                v-model:sorted="sortedCompanyObj"
                @pageNull="pagination.currentPage = 0"
                />

                <table-body
                :companys="paginationReturn"
                @remove="removeCompany"
                v-model:currentPage="pagination.currentPage"
                />
            </table>

            <table-clear
            v-if="searchCompany.length === 0"
            :searchNull="searchValue.length > 0"
            />

            <pagination-block
            v-model:currentValue="pagination.currentPage"
            :maxPage="maxPage"
            class="page-navigation"
            v-if="searchCompany.length !== 0"
            />

        </div>
    </div>
</template>

<script>
    import TableHead from '@/components/TableHead';
    import TableBody from '@/components/TableBody';
    import CreateCompany from '@/components/CreateCompany';
    import TableClear from '@/components/TableClear';
    import PaginationBlock from '@/components/PaginationBlock'
    import companysArray from '@/dataBase.json';

    export default {
        components: { TableHead, TableBody, CreateCompany, TableClear, PaginationBlock },
        data() {
            return {
                companys: companysArray,
                searchValue: '',
                addCompanyModalShow: false,
                sortedCompanyObj: {
                    reverse: false,
                    typeSort: '',
                },
                pagination: {
                    currentPage: 0,
                    defaultSize: 5,
                }
            }
        },
        methods: {
            removeCompany(event) {
                this.companys = this.companys.filter(c => c.id !== event.id);
            },
            createCompany(event){
                this.companys.push(event);
            },
        },
        computed: {
            sortedCompany(){
                return [...this.companys].sort((a, b) => {
                    if(this.sortedCompanyObj.reverse){
                        return b[this.sortedCompanyObj.typeSort]?.localeCompare(a[this.sortedCompanyObj.typeSort]);
                    }
                    else {return a[this.sortedCompanyObj.typeSort]?.localeCompare(b[this.sortedCompanyObj.typeSort]);};
                });
            },
            searchCompany(){
                return this.sortedCompany.filter(c => c.directorName.toLowerCase().includes(this.searchValue.toLowerCase()));
            },
            maxPage(){
                return Math.ceil(this.searchCompany.length / this.pagination.defaultSize) - 1;
            },
            paginationReturn(){
                const start =  this.pagination.currentPage * this.pagination.defaultSize;
                const end =  start + this.pagination.defaultSize;
                return this.searchCompany.slice(start, end);
            }
        }
    }
</script>

<style lang="scss">
    body{
        font-family: 'Inter', sans-serif;
        font-size: 14px;
        font-weight: normal;
        overflow-x: hidden;
    }

    .unselectable {
        -webkit-touch-callout: none;
        -webkit-user-select: none;
        -khtml-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
    }

    .app{
        padding: 50px 0;
    }

    .app-content{
        width: 50%;
        margin: 0 auto;
    }

    th, td, .inp, .btn{
        border: 1px solid #4F4F4F;
        padding: 13px 20px;
    }

    .table{
        width: 100%;
        table-layout: fixed;
    }

    .action-content{
        display: flex;
        justify-content: space-between;
        margin-bottom: 20px;
    }

    .page-navigation{
        margin-top: 20px;
    }
</style>