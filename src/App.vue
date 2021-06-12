<template>
  <div class="container">
    <global-header :user="user"></global-header>
    <!-- <column-list :list ="list"></column-list>  -->
    <form>
      <div class="mb-2">
        <label class="form-label">Email adress</label>
        <validate-input :rules="emailRules" v-model="emailVal" class="placeHolder" placeHolder="Enter email" strictMax=11></validate-input>
      </div>
      <div class="mb-2">
        <label class="form-label">Password</label>
        <validate-input :rules="passwordRules" v-model="passwordVal" class="placeHolder" placeHolder="Enter password" strictMax=20></validate-input>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
// import ColumnList, { ColumnProps } from './components/ColumnList.vue'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
// const testData: ColumnProps[] = [
//   {
//     id: 1,
//     title: 'test1的专栏',
//     description: '这是的test1专栏，有一段非常有意思的简介，可以更新一下欧',
//     avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
//   },
//   {
//     id: 2,
//     title: 'test2的专栏',
//     description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧',
//     avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
//   },
//   {
//     id: 2,
//     title: 'test2的专栏',
//     description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧'
//     // avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
//   },
//   {
//     id: 2,
//     title: 'test2的专栏',
//     description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧',
//     avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
//   }
// ]
const userInfo: UserProps = {
  isLogin: true,
  name: 'pogo',
  id: 3
}
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader,
    ValidateInput
  },
  setup () {
    const emailVal = ref('')
    const passwordVal = ref('')
    const emailRules: RulesProp = [
      { type: 'required', message: 'Email must not be empty!' },
      { type: 'email', message: 'email format must be correct!' }
    ]
    const passwordRules: RulesProp = [
      { type: 'required', message: 'Password must not be empty!' },
      { type: 'range', message: 'Password length should be between 6 and 8, and cannot contain spaces', min: { length: 6 }, max: { length: 10 } }
    ]
    return {
      emailRules: emailRules,
      passwordRules: passwordRules,
      // list: testData,
      user: userInfo,
      emailVal,
      passwordVal
    }
  }
})
</script>

<style>

</style>
