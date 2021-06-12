<template>
  <div class="container">
    <global-header :user="user"></global-header>
    <router-view></router-view>
    <footer class="text-center py-4 text-secondary bg-light mt-6">
      <small>
        <ul class="list-inline mb-0">
          <li class="list-inline-item">©2021 Pogo Blog · </li>
          <li class="list-inline-item">Lesson · </li>
          <li class="list-inline-item">Document · </li>
          <li class="list-inline-item">Contact Us · </li>
          <li class="list-inline-item">More</li>
        </ul>
      </small>
    </footer>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
const userInfo: UserProps = {
  isLogin: false,
  name: 'pogo',
  id: 3
}
export default defineComponent({
  name: 'App',
  components: {
    // ColumnList,
    GlobalHeader
  },
  setup () {
    return {
      user: userInfo
    }
  }
})
</script>

<style>

</style>
