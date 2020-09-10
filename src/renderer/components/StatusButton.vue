<template>
   <el-button 
   type = "type" 
   text = "text" 
   icon = "icon"
   size = "size">
        {{text}}
    </el-button>
</template>
<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'StausButton',
  data: function () {
    return {
       type : 'primary',
       text : '',
       icon : '',
       size : 'medium'
    }
  },
  methods: {
   

  },

})
</script>