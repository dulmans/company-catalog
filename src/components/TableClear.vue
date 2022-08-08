<template>
    <div class="list-null">
        <transition name="list-null">
            <span v-if="searchNull">
                Ничего не найдено &#128532;, попробуйте изменить поисковой запрос
            </span>
            <span v-else>
                Справочник пуст, добавьте организацию, нажав на кнопку "Добавить"
            </span>
        </transition>
    </div>
</template>

<script>
    export default {
        props: {
            searchNull: {
                type: Boolean,
            }
        }
    }
</script>

<style lang="scss" scoped>
    .list-null{
        margin-top: 15px;
        text-align: center;
        font-size: 18px;
        font-weight: 600;
        color:cornflowerblue;
        opacity: .7;
        span{
            display: inline-block;
        }
    }

    .list-null-enter-active,
    .list-null-leave-active {
        transition: transform .2s ease-in-out;
    }

    .list-null-enter-from,
    .list-null-leave-to {
        transform: scale(0);
    }
</style>