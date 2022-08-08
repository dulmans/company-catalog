<template>
    <form class="create-company__form" @submit.prevent>
        <h2>Добавить организацию</h2>
        <div class="input__group">
            <my-input
            placeholder="Название"
            v-model.trim="createCompany.companyName"
            @focus="errors = []"
            />

            <my-input
            placeholder="Номер телефона в формате 79...."
            type="number"
            maxlength="11"
            v-model.trim="createCompany.phoneNumber"
            @focus="errors = []"
            />

            <my-input
            placeholder="ФИО директора"
            v-model.trim="createCompany.directorName"
            @focus="errors = []"
            />
        </div>
        <div class="btn__group">
            <my-button
            @click.stop="$emit('update:show', false)"
            >ОТМЕНА
            </my-button>

            <my-button
            @click.stop="create"
            >ОК</my-button>
        </div>

        <transition name="errors-list">
            <div
            v-if="errors.length > 0"
            class="errors-contain"
            >
                <span v-for="error in errors">{{ error }}</span>
            </div>
        </transition>

    </form>
</template>

<script>
    export default {
        data(){
            return {
                createCompany: {
                    companyName: '',
                    phoneNumber: '',
                    directorName: '',
                },
                errors: [],
            }
        },
        props: {
            show: {
                type: Boolean
            }
        },
        methods: {
            create() {
                this.errors = [];
                if(this.createCompany.companyName.length < 4){this.errors.push('Введите корректное имя организации')}
                if(this.createCompany.phoneNumber.length !== 11){this.errors.push('Введите корректный номер телефона в формате: 79...')}
                if(this.createCompany.directorName.length < 3){this.errors.push('Введите корректное ФИО директора')}
                if(this.errors.length === 0){
                    this.createCompany.id = Date.now();
                    this.createCompany.phoneNumber = '+' + this.createCompany.phoneNumber;
                    this.$emit('create', this.createCompany);
                    this.$emit('update:show', false);
                    this.createCompany = {
                        companyName: '',
                        phoneNumber: '',
                        directorName: '',
                    }
                }
            }
        },
    }
</script>

<style lang="scss" scoped>
    .create-company__form {
        margin: 0 -20px;
        & > * {
            padding: 0 20px;
        }
    }

    h2{
        font-size: 24px;
        font-weight: 600;
        color: slategrey;
    }

    .input__group{
        display: flex;
        flex-direction: column;
        border-top: 2px solid #4F4F4F;
        border-bottom: 2px solid #4F4F4F;
        margin: 10px 0;
        padding: 10px 20px;
        & > *:not(:last-child){
            margin-bottom: 10px;
        }
    }

    .btn__group{
        display: flex;
        justify-content: center;
        & > *{
            width: 100px;
            &:nth-child(1){
                margin-right: 15px;
            }
        }
    }

    .errors-contain{
        margin-top: 15px;
        display: flex;
        flex-direction: column;
        color: darkred;
        text-align: center;
        max-width: fit-content;
        > *:not(:last-child){
            margin-bottom: 10px;
        }
    }

    .errors-list-enter-active, .errors-list-leave-active {
        transition: transform 0.4s ease;
    }

    .errors-list-enter-from, .errors-list-leave-to {
        transform: scale(0);
    }
</style>