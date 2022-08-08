<template>
    <tbody class="table-body">

    <transition-group name="company-list">
        <company-item
        v-for="company in companys"
        :company="company"
        :key="company.id"
        @remove="removes(company)"
        />
    </transition-group>

    </tbody>
</template>

<script>
    import CompanyItem from '@/components/CompanyItem';
    export default {
        components: { CompanyItem },
        props: {
            companys: {
                type: Array,
                default: () => [],
                required: true
            },
            currentPage: {
                type: Number,
            }
        },
        methods: {
            removes(item){
                this.$emit('remove', item);
                if(this.companys.length === 1 && this.currentPage !== 0){
                    this.$emit('update:currentPage', this.currentPage - 1);
                }
            }
        },
    }
</script>

<style lang="scss" scoped>
    .list-null{
        font-size: 18px;
        font-weight: 600;
        width: 100%;
    }

    .company-list-item {
        display: inline-block;
        margin-right: 10px;
    }

    .company-list-enter-active,
    .company-list-leave-active {
        transition: all .4s ease;
    }

    .company-list-enter-from,
    .company-list-leave-to {
        opacity: 0;
        transform: translateX(130px);
    }

    .company-list-move {
        transition: transform .4s ease;
    }
</style>