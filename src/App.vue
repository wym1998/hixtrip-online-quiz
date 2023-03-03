<script setup lang="ts">
import { onMounted, Ref, ref } from "vue";
import userApi from "./api/user";
import orgApi from "./api/org";
import OrgTree from './components/orgTree.vue'
import UserTable from './components/userTable.vue'
let user = ref<any>();
let org = ref<any>();
const data = ref<any>();



onMounted(() => {
  // 输入查询数据获取
  userApi.query({}).then((res) => {
    user.value = res;
  });
  // 树状数据获取
  orgApi.query().then((res) => {
    org.value = res;
    org.value = org.value.map((i: any) => {
      return {
        label: i.id,
        children: [
          {
            label: i.name,
            
          },
        ],
      };
    });
    data.value = org.value;
    
  });
});
</script>

<template>
  <div>
    <!-- {{ org org}} -->
    <!-- {{ user }} -->
    
    <!-- 树状节点组件 -->
    <OrgTree :data="data"></OrgTree>

    <!-- 查询表格组件 -->
    <UserTable v-if="user" :msg="user" ></UserTable>
   
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
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
