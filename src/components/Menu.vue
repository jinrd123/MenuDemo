<template>
  <div class="menu-container">
    <ul class="menu-ul">
      <li 
        v-for="(menuItem, index) in menuList" 
        :key="index"
        @click="changeMenu(index)"
        :class="{
          'active-li': index===activeIndex
        }"
      >
        {{ menuItem }}
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref} from "vue";
export default defineComponent({
  name: "Menu",
  props: {
    menuList: {
      type: Array as PropType<string[]>,
      default() {
        return [
          "产品&市场",
          "技术&研发",
          "管理&职场",
          "活动&生活",
          "其他",
        ];
      },
    },
    activeMenuItem: {
      type: String
    }
  },
  emits: ["update:activeMenuItem", "changeMenu"],
  setup(props, {emit}) {
    // 选中导航的标识变量
    const activeIndex = ref(0);
    // 切换导航的回调
    const changeMenu = (index: number) => {
      activeIndex.value = index;
      emit("update:activeMenuItem", props.menuList[index]);
      emit("changeMenu");
    }
    return {
      changeMenu,
      activeIndex
    };
  },
});
</script>

<style scoped lang="less">
.menu-container {
  .menu-ul {
    display: flex; // 布局属性: li标签一行排列
    column-gap: 50px; // 样式属性: 控制选项间隙，在flex项目与项目之间添加间隙
    li {
      list-style-type: none; // 样式属性: 去除li标签的默认小圆点样式
      background-image: linear-gradient(
        90deg,
        red,
        green
      ); // 样式属性: 方便观察
      &.active-li {
        background-image: linear-gradient(
          270deg,
          red,
          green
        );
      }
    }
  }
}
</style>
