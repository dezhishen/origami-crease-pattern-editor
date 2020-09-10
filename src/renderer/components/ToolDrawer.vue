<template>
     <el-drawer
    title = "工具test"
    :visible.sync = 'drawer'
    direction = "ttb"
    :modal = false
    :modal-append-to-body = false
    :wrapperClosable = false
    size="20%"
    :before-close = "handleClose">
        <span>我来啦!</span>
    </el-drawer>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  data: function () {
    return {
        
    }
  },
  props: {
      drawer: Boolean
  },
  methods: {
    handleClose(done) {
        this.$confirm('确认关闭？')
          .then(_ => {
            this.drawer = false;
            done();
          })
          .catch(_ => {});
      },
    setDrawer(val){
        this.drawer = val;
    },
  },
  mounted: function () {
    
  },
})
</script>

<style>


</style>