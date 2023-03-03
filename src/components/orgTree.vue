<template>
  <div>
    <h3>树状节点</h3>
    <el-tree :data="data" :props="defaultProps"  @node-click="handleNodeClick" />
  </div>
</template>

<script setup lang="ts">
import {defineProps} from 'vue'
interface Tree {
  label: string;
  children?: Tree[];
}
const defaultProps = {
  children: "children",
  label: "label",
};

// 接受父组件传来的值
 const props = defineProps({
    data:Array
 })
 const handleNodeClick = (data: Tree) => {};
</script>

<style>

</style>