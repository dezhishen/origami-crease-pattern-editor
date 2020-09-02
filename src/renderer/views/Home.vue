<template>
  <div style="margin-top:5px;margin-bottom:5px">
    <el-container>
      <el-header style="height:35px">
        <el-button type="text" size="small">导入</el-button>
        <el-button type="text" @click="handleExport" size="small">导出</el-button>
        <el-button type="text" size="small">折叠</el-button>
      </el-header>
      <el-container>
        <el-aside style="width:70px">
          <div style="margin-left:5px">
            <el-row>
              <el-button type="text" size="small">峰线</el-button>
            </el-row>
            <el-row>
              <el-button type="text" size="small">谷线</el-button>
            </el-row>
            <el-row>
              <el-button type="text" size="small">辅助线</el-button>
            </el-row>
          </div>
        </el-aside>
        <el-main>[][][]</el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'Home',
  data: function () {
    return { title: '~' }
  },
  methods:{
    handleExport:function(){
      console.log("我是导出方法")
    }
  },
  mounted:function(){
    //todo init p2
  }
})
</script>

<style>
</style>
