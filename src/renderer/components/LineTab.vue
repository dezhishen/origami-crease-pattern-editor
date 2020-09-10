<template>
    <el-tab-pane name="line"  label="线编辑" >
        <el-checkbox v-model="addline" icon="el-icon-edit" border  label="添加线"> </el-checkbox>
        <el-checkbox v-model="delline" icon="el-icon-edit" border  label="删除线"> </el-checkbox>
    </el-tab-pane>
</template>
<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'LineTab',
  data: function () {
    return {
        addline : false,
        delline : false,
    }
  },
  methods: {
   

  },

})
</script>