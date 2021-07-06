<template>
<div class="container">
  <global-header :user="currentUser"></global-header>
  <!-- <column-list :list="list"></column-list> -->
  <validate-form @form-submit="onFormSubmit">
    <div class="mb-2">
      <label class="form-label">邮箱地址</label>
      <validate-input :rules="emailRules" v-model="emailVal" placeholder="请输入邮箱地址" type="text"></validate-input>
      {{emailVal}}
    </div>
  <div class="mb-2">
    <label for="exampleInputPassword1" class="form-label">密码</label>
    <input type="password" class="form-control" id="exampleInputPassword1">
  </div>
  <div class="mb-2 form-check">
    <input type="checkbox" class="form-check-input" id="exampleCheck1">
    <label class="form-check-label" for="exampleCheck1">Check me out</label>
  </div>
  <template #submit><span class="btn btn-danger">登陆</span></template>
</validate-form>
</div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateForm from './components/ValidateForm.vue'
const currentUser: UserProps = {
  isLogin: true,
  name: 'wiki bill'
}
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: '这是test1专栏,有一段非常有意思的简介,可以更新一下哦',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 2,
    title: 'test2的专栏',
    description: '这是test2专栏,有一段非常有意思的简介,可以更新一下哦'
    // avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 3,
    title: 'test3的专栏',
    description: '这是test3专栏,有一段非常有意思的简介,可以更新一下哦',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 4,
    title: 'test3的专栏',
    description: '这是test3专栏,有一段非常有意思的简介,可以更新一下哦',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  }
]
const emailReg = /^[A-Za-z0-9\u4e00-\u9fa5]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader,
    ValidateInput,
    ValidateForm
  },
  setup () {
    const emailVal = ref('')
    const emailRules: RulesProp = [
      { type: 'required', message: '电子邮箱地址不能为空' },
      { type: 'email', message: '请输入正确的电子邮箱格式' }
    ]
    const emailRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const validateEmail = () => {
      if (emailRef.val.trim() === '') {
        emailRef.error = true
        emailRef.message = 'can not be empty'
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true
        emailRef.message = 'should be valid email'
      }
    }
    const onFormSubmit = (result: boolean) => {
      console.log('123', result)
    }
    return {
      list: testData,
      currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal,
      onFormSubmit
    }
  }
})
</script>

<style>

</style>
