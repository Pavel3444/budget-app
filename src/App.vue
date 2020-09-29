<template>
    <div id="app">
        <Form :total="totalBalance" @submitForm="onFormSubmit"/>
        <TotalBalance :total="totalBalance"/>
        <BudgetList :list="list" @deleteItemParent="deleteItemParent" />

    </div>
</template>

<script>
    import BudgetList from "./components/BudgetList";
    import TotalBalance from "./components/TotalBalance";
    import Form from "./components/Form";

    export default {
        name: 'App',
        components: {
            BudgetList,
            TotalBalance,
            Form
        },
        data() {
            return {
                list: {
                    1: {
                        type: 'INCOME',
                        value: 100,
                        comment: 'some comments',
                        id: 1,
                    },
                    2: {
                        type: 'OUTCOME',
                        value: -50,
                        comment: 'some outcome comments',
                        id: 2,
                    },
                },
            }

        },
        computed: {
            totalBalance() {
                return Object.values(this.list).reduce((acc, item) => acc + item.value, 0);

            }
        },
        methods: {
            deleteItemParent(id) {
                const i = confirm('удалить?');
                if (i){
                    this.$delete(this.list, id);
                }
            },
            onFormSubmit(data) {
                console.log(typeof data.value);
                if (data.type === 'OUTCOME' && data.value[0] !== '-' ){

                    data.value = Number(`-${data.value}`);
                }

                const newObj = {
                    ...data,
                    id: String(Math.random())
                };
                this.$set(this.list, newObj.id, newObj);
            },
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
