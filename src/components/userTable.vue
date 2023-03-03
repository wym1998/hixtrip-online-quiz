<template>
  <div>
    <h3>输入查询</h3>
    <div class="search">
      <input v-model="keyword" type="text" placeholder="输入搜索关键字" />
      <div class="btn" @click="onSearch">查询</div>
    </div>
    <table border="1" class="box">
      <tr>
        <th>id</th>
        <th>姓名</th>
      </tr>
      <tr v-for="(item, index) in newData" :key="index">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
      </tr>
    </table>
  </div>
</template>

<script setup lang="ts">
import { Ref, ref, defineProps } from "vue";

// 接受父组件传来的值
let props = defineProps({
    msg: Array,
});
let keyword = ref<any>();
let newData = ref<any>();
newData.value = props.msg;
// 关键词查询
const onSearch = () => {
    newData.value = newData.value.filter(
      (item: { name: any }) => keyword.value == item.name
    );
};
</script>

<style scoped>
.box {
  border-collapse: collapse;
}
.search {
  margin-bottom: 20px;
  width: 500px;
  display: flex;
  justify-content: space-around;
}
.search .btn {
  width: 100px;
  text-align: center;
  border: 1px solid;
}
</style>