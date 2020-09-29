<template>
    <ElCard class="formCard">
        <ElForm :model="formData" ref="addItemForm" :rules="rules" label-position="top">
            <ElFormItem label="Type" prop="type">
                <ElSelect class="type-select" v-model="formData.type" placeholder="Choose type...">
                    <ElOption label="Income" value="INCOME"/>
                    <ElOption label="Outcome" value="OUTCOME"/>
                </ElSelect>
            </ElFormItem>
            <ElFormItem label="Comments" prop="comment">
                <ElInput v-model="formData.comment"/>
            </ElFormItem>
            <ElFormItem label="Value" prop="value">
                <ElInput v-model.number="formData.value"/>
            </ElFormItem>
            <ElButton type="primary" @click="onSubmit">Submit</ElButton>

        </ElForm>
    </ElCard>
</template>

<script>
    export default {
        name: "Form",
        data: () => ({
            formData: {
                type: 'INCOME',
                comment: "",
                value: 0
            },
            rules: {
                type: [
                    {required: true, message: "Please select type", trigger: "blur"}
                ],
                comment: [
                    {required: true, message: "Please input comment", trigger: "change"}
                ],
                value: [
                    {required: true, message: "Please input value", trigger: "change"},
                    {type: 'number', message: 'Value not a number', trigger: 'change'}
                ]
            }
        }),
        props: {
            total: {
                type: Number,
                default: 0
            }
        },
        methods: {
            onSubmit() {
                this.$refs.addItemForm.validate(valid => {
                    // console.log(valid);
                    if (valid) {
                        this.$emit('submitForm', {...this.formData});
                        this.$refs.addItemForm.resetFields();
                    }
                });
                setTimeout( () => {
                    const sumBlock = document.querySelector('.total-value');
                   this.total > 0 ? sumBlock.style.color = "green" : this.total < 0 ? sumBlock.style.color = "red" : sumBlock.style.color = "black";
                    }, 100 )
            }
        }
    }
</script>

<style scoped>
    .formCard {
        max-width: 500px;
        margin: auto;
    }

    .type-select {
        width: 100%;
    }
</style>
