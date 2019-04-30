<template>
    <el-container>
        <el-header style="font-size: x-large;text-align: center">欢迎报名{{activity.name}}活动</el-header>
        <el-form ref="form" :model="form" label-width="50px" label-position="top">
            <el-form-item label="姓名">
                <el-input clearable maxlength=10 prefix-icon="el-icon-user-solid"
                          v-model="form.name"></el-input>
            </el-form-item>
            <el-form-item label="手机号码">
                <el-input clearable maxlength=11 prefix-icon="el-icon-phone"
                          v-model="form.phone"></el-input>
            </el-form-item>
            <el-form-item label="身份证号码">
                <el-input clearable maxlength=18 prefix-icon="el-icon-s-check"
                          v-model="form.idCard"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="onSubmit" style="width: 100%" :loading="loading">报名</el-button>
            </el-form-item>
        </el-form>
    </el-container>
</template>

<script>
    export default {
        data() {
            return {
                form: {
                    name: '',
                    phone: '',
                    idCard: ''
                },
                loading: false,
                activity: {
                    id: '',
                    name: '火星冒险'
                }
            }
        },
        methods: {
            onSubmit() {
                console.log(this.form);
                if (!this.onValidate()) return;
                this.loading = true;
                setTimeout(() => {
                    this.form = {
                        name: '',
                        phone: '',
                        idCard: ''
                    };
                    this.loading = false;
                    this.$message({
                        message: '报名成功',
                        type: 'success'
                    });
                }, 2000);
            },
            onValidate() {
                if ('' === this.form.name) {
                    this.$message({
                        message: '姓名不能为空',
                        type: 'error'
                    });
                    return false;
                }
                if ('' === this.form.phone) {
                    this.$message({
                        message: '电话号码不能为空',
                        type: 'error'
                    });
                    return false;
                }
                if (!(/^1[34578]\d{9}$/.test(this.form.phone))) {
                    this.$message({
                        message: '手机号码有误',
                        type: 'error'
                    });
                    return false;
                }
                if ('' === this.form.idCard) {
                    this.$message({
                        message: '身份证号码不能为空',
                        type: 'error'
                    });
                    return false;
                }
                if (!(/(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/.test(this.form.idCard))) {
                    this.$message({
                        message: '身份证号码有误',
                        type: 'error'
                    });
                    return false;
                }
                return true;
            }
        }
    }
</script>

<style>

</style>
