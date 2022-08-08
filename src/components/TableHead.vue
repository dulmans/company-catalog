<template>
    <thead
    class="table-head"
    >
        <tr>
            <head-item-sort
            @changeSort="sortedClick('companyName')"
            :sortInfo="{active: sorted.typeSort === 'companyName', reverse: sorted.reverse}"
            >
                Название
            </head-item-sort>

            <head-item-sort
            @changeSort="sortedClick('directorName')"
            :sortInfo="{active: sorted.typeSort === 'directorName', reverse: sorted.reverse}"
            >
                ФИО директора
            </head-item-sort>

            <head-item>Номер телефона</head-item>
            <head-item style="width: 15px;"></head-item>
        </tr>
    </thead>
</template>

<script>
    import HeadItem from '@/components/HeadItem'
    import HeadItemSort from '@/components/HeadItemSort';

    export default {
        components: { HeadItem, HeadItemSort },
        props: {
            sorted: {
                type: Object,
            }
        },
        methods: {
            sortedClick(typeS){
                const returnSorted = {
                    reverse: false,
                    typeSort: typeS
                }
                if(typeS === this.sorted.typeSort){
                    returnSorted.reverse = !(this.sorted.reverse);
                }
                this.$emit('update:sorted', returnSorted);
                this.$emit('pageNull');
            },
            iconSwap(){
            }
        }
    }
</script>