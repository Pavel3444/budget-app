<template>
    <div>
        <div class="list-item" v-for="(item, prop ) in list" :key="prop">
            <span :class="item.type === 'INCOME' ? 'el-icon-top' : 'el-icon-bottom'">  </span>
            <span class="budget-comment">{{item.comment}}</span>
            <span class="budget-value"><b :class="item.type === 'INCOME' ? 'green' : 'red'">{{item.value}}</b></span>
            <ElButton type="danger" size="mini" @click="deleteItemChild(item.id)">Delete</ElButton>
        </div>
    </div>
</template>

<script>
    export default {
        name: "BudgetListItem",
        props: {
            list: {
                type: Object,
                default: () => ({}),
            },
        },
        methods: {
            deleteItemChild(id) {
                this.$emit("onDeleteItem", id);
            },

        },
    }
</script>

<style scoped>
    .list-item {
        display: flex;
        align-items: center;
        padding: 10px 15px;
    }

    .budget-value {
        margin-left: auto;
        margin-right: 20px;
        font-weight: bold;
    }
    .red{
        color: red;

    }
    .green{
        color: green;
    }
</style>
