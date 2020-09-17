<template>
  <div style="height:100%;">
    <el-container>
      <el-container>
        <el-aside>
          <div class = "layer-tree-container">
            <div class = "tree-head-label">
              <span class = "title-span">图层控制</span>
            </div>
            <layer-tree @treeNodeClick="handelLayerChange"></layer-tree>
          </div>
          <div style="height:65%;">
            <el-tabs type="border-card" v-model="activeTab" style="height:100%;">
              
              <el-tab-pane name="layerTool" label="图层工具">
                <grid-tab v-show = "gridVis"></grid-tab>
                <line-tab v-show = "lineVis"></line-tab>
                <point-tab v-show = "pointVis"></point-tab>
              </el-tab-pane>
              <el-tab-pane name="canvasTool" label="画布工具">比如 撤销 重做 平移 缩放 旋转</el-tab-pane>  
              <!-- <el-tab-pane name="chooseTool" label="选择工具" style="display:none;">支持点选 框选 然后操作选中要素</el-tab-pane> -->
            </el-tabs>
          </div>
        </el-aside>
        <div class ="layer-tree-switch" @click="handleTreeVis">
          <i class="el-icon-arrow-left" style="padding-top:12px;"></i>
        </div>
        <fabric-canvas></fabric-canvas>

      </el-container>
    </el-container>
  </div>
</template>

<script>
import Vue from 'vue'
import LayerTree from '../components/LayerTree.vue'
import GridTab from '../components/GridTab.vue'
import LineTab from '../components/LineTab.vue'
import PointTab from '../components/PointTab.vue'
import FabricCanvas from  '../components/Canvas.vue'
export default Vue.extend({
  name: 'Home',
  components: {
    LayerTree,
    GridTab,
    LineTab,
    PointTab,
    FabricCanvas,
  },
  data: function () {
    return {
      activeTab: 'none',
      gridVis:false,
      lineVis:false,
      pointVis:false,
      curLayerId: -1,
      carvans: null,
      groups:{
        "id":"group"
      }
    }
  },
  methods: {
    handelLayerChange(val) {
      this.curLayerId = val;
      this.gridVis = false;
      this.lineVis = false;
      this.pointVis = false;
      if(val == 1){
        return;
      }else if(val == 2){
        this.gridVis = true;
      }else if(val > 3 ){
        this.lineVis = true;
      }else{
        this.pointVis = true;
      }


      console.log(this.curLayerId );
    },
    handleTreeVis() {
      console.log(111)
    },


  },
  mounted: function () {
  
  },
})
</script>

<style scoped>
.el-container {
  height: 100%;
}
.el-aside{
  width:270px;
  border:2px solid silver;
  height:100%;
}

.el-main{
  padding:0px;
  overflow: hidden;
}

.layer-tree-container{
  height:35%;
  overflow:auto;
}
.tree-head-label{
  height:auto;
  background-color: rgba(49, 110, 175, 0.95);
}
.title-span{
  margin-left:10px;
  color: white;
}

.layer-tree-switch{
  overflow: hidden;
  z-index: 9999;
  position: fixed;
  left:270px;
  top:30%;
  background-color:silver;
  height:40px;
  border-bottom-right-radius: 4px;
  border-top-right-radius: 4px;
  display: none;
}

</style>
