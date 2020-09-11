<template>
    <el-tab-pane name="line"  label="线编辑" >
      <el-row>
        <el-col :span="12">
          <el-checkbox-group  v-model="cbgAddLine" text-color="white" fill="green">
            <el-checkbox-button :checked="addline"><i :class = "icon[0]" style="padding-right:5px"></i>{{text[0]}}</el-checkbox-button>
          </el-checkbox-group>
        </el-col>
      
        <el-col :span="12">
          <el-checkbox-group  v-model="cbgDelLine" text-color="white" fill="red" style="width:60px">
            <el-checkbox-button :checked="delline" ><i :class = "icon[1]" style="padding-right:5px"></i>{{text[1]}}</el-checkbox-button>
          </el-checkbox-group>
        </el-col>
      
      </el-row>
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
        text: ['添加线','删除线'],
        icon: ['el-icon-edit','el-icon-delete'],
        cbgAddLine: [],
        cbgDelLine: [],
    }
  },
  methods: {
   

  },

})
</script>
<style scoped>
  .el-checkbox-group{
    margin-right: 25px;
  }


</style>>