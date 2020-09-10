<template>
    <el-tab-pane name="point"  label="点编辑" >
        <el-checkbox v-model="addpoint" icon="el-icon-edit" border  label="添加点"> </el-checkbox>
        <el-checkbox v-model="delpoint" icon="el-icon-edit" border  label="删除点"> </el-checkbox>
        <st-button :text = "text" :type = "type"></st-button>
    </el-tab-pane>
</template>
<script>
import Vue from 'vue'
import StButton from '../components/StatusButton.vue'

export default Vue.extend({
  name: 'PointTab',
  components:{
      StButton,
  },
  data: function () {
    return {
        addpoint:false,
        delpoint:false,
        text: 'test',
        type:  "primary",
    }
  },
  methods: {
   

  },

})
</script>