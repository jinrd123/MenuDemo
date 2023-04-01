<template>
  <Menu 
    v-model:activeMenuItem="activeMenuInfo" 
    :menuList="menuList"
    @changeMenu="test"
  />
</template>

<script setup lang="ts">
import Menu from "@/components/Menu.vue";
import {ref, watch} from "vue";
const menuList = ["产品&市场", "技术&研发", "管理&职场", "活动&生活", "其他"];
const activeMenuInfo = ref(menuList[0]); // activeMenuInfo初始化值理论上应为传给Menu组件的渲染列表的第一项
watch(activeMenuInfo, (newValue, oldValue) => {
  console.log(newValue, oldValue);
})
const test = () => {
  console.log("父组件中切换导航的回调函数");
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>
