<template>
    <div class="login-box">
        <el-form ref="ruleFormRef" :model="ruleForm" status-icon :rules="rules" label-width="120px"
            class="demo-ruleForm">
            <el-form-item label="账号：" prop="userName">
                <el-input v-model="ruleForm.userName" autocomplete="off" />
            </el-form-item>
            <el-form-item label="密码：" prop="psaaWord">
                <el-input v-model="ruleForm.passWord" type="password" autocomplete="off" />
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="submitForm(ruleFormRef)">登陆</el-button>
                <el-button @click="resetForm(ruleFormRef)">重置</el-button>
            </el-form-item>
        </el-form>

        <WavesCanves class="wavesCanves" />
    </div>
</template>


<script lang="ts" setup>
import { reactive, ref } from 'vue'
import WavesCanves from '@/components/WavesCanves.vue' //浪花
import type { FormInstance } from 'element-plus'

const ruleFormRef = ref<FormInstance>()

const ruleForm = reactive({
    userName: '',
    passWord: '',
})

const rules = reactive({
    userName:
        [
            //required 是否必填 这里的message 没有填出来的展示信息
            { required: true, message: '请输入你的账号', trigger: 'blur' },
            //下面的message 没有达到要求展示的信息
            { min: 3, max: 10, message: '账号的长度在3~10之间', trigger: 'blur' },
        ],
    passWord:
        [
            { required: true, message: '请输入你的密码', trigger: 'blur' },
            { min: 3, max: 10, message: '账号的长度在3~10之间', trigger: 'blur' },
        ],
})

const submitForm = (formEl: FormInstance | undefined) => {
    if (!formEl) return
    formEl.validate((valid) => {
        if (valid) {
            console.log('submit!')
        } else {
            console.log('error submit!')
            return false
        }
    })
}

const resetForm = (formEl: FormInstance | undefined) => {
    if (!formEl) return
    formEl.resetFields()
}
</script>

<style scoped lang='scss'>
.login-box {
    width: 100%;
    height: 100%; //宽高设置100%，保证图片能百分百撑满背景
    background: rgb(238, 174, 202);
    background: radial-gradient(circle, rgba(238, 174, 202, 1) 0%, rgba(148, 187, 233, 1) 100%);
}

.wavesCanves {
    width: 100%;
    height: 100%;
    position: fixed;
    bottom: -250px;

}
</style>