<script setup lang="ts">


import {ref} from "vue";
import myAxios from "../plugins/myAxios";
import {Toast} from "vant";


const userAccount = ref('')
const userPassword = ref('')
const RePassword = ref('')
const planetCode = ref('')
const onSubmit = async (values : any) => {
  const res = await myAxios.post('/user/register', {
    userAccount: userAccount.value,
    userPassword: userPassword.value,
    checkPassword: RePassword.value,
    planetCode: planetCode.value
  })

  if (res.code === 0 && res.data) {
    Toast.success("注册成功!")
    const redirectUrl = window.location.href;
    window.location.href = `/user/login?redirect=${redirectUrl}`;
  } else {
    Toast.fail("注册失败！" + res.description);
  }
};

</script>

<template>
  <van-form @submit="onSubmit">
    <van-cell-group inset>
      <van-field
          v-model="userAccount"
          name="账户"
          label="账户"
          placeholder="账户"
          :rules="[{ required: true, message: '请填写账户' }]"
      />
      <van-field
          v-model="userPassword"
          type="password"
          name="密码"
          label="密码"
          placeholder="密码"
          :rules="[{ required: true, message: '请填写密码' }]"
      />
      <van-field
          v-model="RePassword"
          type="password"
          name="确认密码"
          label="确认密码"
          placeholder="确认密码"
          :rules="[{ required: true, message: '请填写密码' }]"
      />
      <van-field
          v-model="planetCode"

          name="星球账号"
          label="星球账号"
          placeholder="星球账号"
          :rules="[{ required: true, message: '请填写星球账号' }]"
      />
    </van-cell-group>
    <div style="margin: 16px;">
      <van-button round block type="primary" native-type="submit">
        提交
      </van-button>

    </div>
  </van-form>
</template>

<style scoped>

</style>