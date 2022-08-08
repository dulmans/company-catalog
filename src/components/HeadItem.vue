<template>
    <th
    class="table-head__item unselectable"
    >
        <slot></slot>
    </th>
</template>

<style lang="scss" scoped>
    .table-head__item {
        background: rgb(244, 248, 249);
        color: #4F4F4F;
        font-weight: 600;
        font-size: 18px;
        letter-spacing: 1px;
    }
</style>