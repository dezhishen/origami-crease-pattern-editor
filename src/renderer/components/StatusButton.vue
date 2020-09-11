<template>
   <el-button 
   :type = "checked ? type :''" 
   :text = "text" 
   :size = "size"
   @click="handleClick">
        <i :class = "icon"></i> {{text}}
    </el-button>
</template>
<script>
import { check } from 'prettier'
import Vue from 'vue'

export default Vue.extend({
  name: 'StausButton',
  data: function () {
    return {
      checked: false,
    }
  },
  props:{
    type :{
      type:String,
      default:'primary',
    } ,
    text:{
      type:String,
      default:'普通按钮',
    } ,
    icon:{
      type:String,
      default: '',
    } ,
    size:{
      type:String,
      default:'large',
    } ,
  },
  methods: {
    handleClick(){
      if(!this.checked){
        this.checked = true;
      }else{
        this.checked = false;
      }
        
    },

  },

})
</script>
<style scoped>

  


</style>>