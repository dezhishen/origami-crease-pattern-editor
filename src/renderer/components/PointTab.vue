<template>
    <el-tab-pane name="point"  label="点编辑" >
      <el-row>
        <el-col :span="12">
          <el-checkbox-group  v-model="cbgAddPoint" text-color="white" fill="green">
            <el-checkbox-button :checked="addpoint" @change="handleAddPt"><i :class = "icon[0]" style="padding-right:5px"></i>{{text[0]}}</el-checkbox-button>
          </el-checkbox-group>
        </el-col>
      
        <el-col :span="12">
          <el-checkbox-group  v-model="cbgDelPoint" text-color="white" fill="red" style="width:60px">
            <el-checkbox-button :checked="delpoint" @change="handleDelPt" ><i :class = "icon[1]" style="padding-right:5px"></i>{{text[1]}}</el-checkbox-button>
          </el-checkbox-group>
        </el-col>
      
      </el-row>
    </el-tab-pane>
</template>
<script>
import Vue from 'vue'
export default Vue.extend({
  name: 'PointTab',
  data: function () {
    return {
        addpoint:false,
        delpoint:false,
        text: ['添加点','删除点'],
        type: ['primary','danger'],
        icon: ['el-icon-edit','el-icon-delete'],
        cbgAddPoint: [],
        cbgDelPoint: [],
    }
  },
  methods: {
    handleAddPt(){
      if(!this.addpoint){
        this.addpoint = true;
        this.delpoint = false;
        this.cbgDelPoint = [];
      }else{
        this.addpoint = false;
      }
    },
    handleDelPt(){
      if(!this.delpoint){
        this.delpoint = true;
        this.addpoint = false;
        this.cbgAddPoint = [];
      }else{
        this.delpoint = false;
      }
    },

  },

})
</script>