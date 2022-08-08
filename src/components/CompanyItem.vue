<template>
        <tr>
            <td>{{ company.companyName }}</td>
            <td>{{ company.directorName }}</td>
            <td>{{ company.phoneNumber }}</td>
            <td
            class="delete-btn"
            @click="$emit('remove', company)"
            >
                <div class="line">
                    <span class="ones-line"></span>
                    <span class="twos-line"></span>
                </div>
            </td>
        </tr>
</template>

<script>
    export default {
        props: {
            company: {
                type: Object,
                required: true,
            }
        }
    }
</script>

<style lang="scss" scoped>
    td{
        white-space: nowrap;
        text-overflow: ellipsis;
        overflow: hidden;
        color: #0C0C0C;
        font-weight: 400;
        letter-spacing: .4px;
        font-size: 16px;
    }

    .delete-btn{
        padding: 0;
        position: relative;
        cursor: pointer;
        .line{
            display: flex;
            justify-content: center;
            align-items: center;
            margin-bottom: 5px;
            transition: all .18s linear;
            span{
                position: absolute;
                display: inline-block;
                width: 2px;
                height: 70%;
                background: darkred;
                border-radius: 20px;
                border: 1px solid darkred;
                transition: all .3s ease-in-out;
            }
            .ones-line{
                transform: rotate(-45deg);
            }
            .twos-line {
                transform: rotate(45deg);
            }
        }
        &:hover .line{
            opacity: .7;
        }
        &:active .line{
            .ones-line{
                transform: rotate(0deg);
            }
            .twos-line {
                transform: rotate(0deg);
            }
        }
    }
</style>