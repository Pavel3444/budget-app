<template>
    <div class="budget-list-wrap">
        <ElCard :header="header">
            <template v-if="!isEmpty">
                <BudgetListItem :list="list" @onDeleteItem="onDeleteItem"/>

            </template>
            <ElAlert v-else :title="emptyList" closable="false"/>

        </ElCard>
    </div>
</template>

<script>
    import BudgetListItem from "./BudgetListItem";

    export default {
        name: "BudgetList",
        props: {
            list: {
                type: Object,
                default: () => ({}),
            },
        },
        components: {
            BudgetListItem
        },
        data: () => ({
            header: "Budget List",
            emptyList: "Empty List"
        }),
        computed: {
            isEmpty() {
                return !Object.keys(this.list).length

            }
        },
        methods: {
            onDeleteItem(id) {
                this.$emit("deleteItemParent", id);
            },
        }
    }
</script>

<style scoped>
    .budget-list-wrap {
        margin: auto;
        max-width: 500px;
    }

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

</style>
