<template>
  <div style="height:100%;">
    <el-container>
      <el-container>
        <el-aside style="width:270px;border:2px solid silver;height:100%;">
          <div style="height:35%;overflow:auto;">
            <div style="height:auto;background-color: rgba(49, 110, 175, 0.95);">
              <span style="margin-left:10px;color: white;">图层控制</span>
            </div>
            <layer-tree @treeNodeClick="handleDrawer"></layer-tree>
          </div>
          <div style="height:65%;">
            <el-tabs type="border-card" v-model="activeTab" style="height:100%;">
             
              <el-tab-pane name="grid" v-if="curLayerId===2" label="网格编辑" >
                <template>
                  <el-form class="demo-form-inline" style="padding-left:10px;">
                    <el-form-item label="等分数">
                      <el-input-number
                        v-model="gridNum"
                        controls-position="right"
                        @change="handleGridChange"
                        :min="0"
                        :max="256"
                        size="small"
                      ></el-input-number>
                    </el-form-item>
                    <el-form-item>
                      <el-button-group>
                        <el-button type="primary" @click="handleGridMultiply">X2</el-button>
                        <el-button type="primary" @click="handleGridDivide">X1/2</el-button>
                        <el-button type="primary" @click="handleGridClear">归零</el-button>
                      </el-button-group>
                    </el-form-item>
                  </el-form>
                </template>
              </el-tab-pane>
              <el-tab-pane name="layerTool" label="画布工具">比如 撤销 重做 平移 缩放 旋转</el-tab-pane>
              <!-- <el-tab-pane name="chooseTool" label="选择工具" style="display:none;">支持点选 框选 然后操作选中要素</el-tab-pane> -->
            </el-tabs>
          </div>
        </el-aside>
        <div
          style="overflow: hidden;z-index: 9999;position: fixed;left:270px;top:30%
         ;background-color:silver;height:40px;border-bottom-right-radius: 4px;border-top-right-radius: 4px;"
          @click="handleTreeVis"
        >
          <i class="el-icon-arrow-left" style="padding-top:12px;"></i>
        </div>
        <el-main style="background-color:#f3f3f3">
          我是画布
        <tool-drawer ref="pointToolBar" ></tool-drawer>
        </el-main>
        
      </el-container>
    </el-container>
  </div>
</template>

<script>
import Vue from 'vue'
import LayerTree from '../components/LayerTree.vue'
import ToolDrawer from '../components/ToolDrawer.vue'

export default Vue.extend({
  name: 'Home',
  components: {
    LayerTree,
    ToolDrawer,
  },
  data: function () {
    let pointDrawer = false;
    return {
      activeTab: 'none',
      curLayerId: 10,
      gridNum: 0,
      pointDrawer:pointDrawer,
    }
  },
  methods: {
    handleGridClear: function () {
      this.gridNum = 0
    },
    handleGridMultiply: function () {
      if (!this.gridNum || this.gridNum === 0) {
        this.gridNum = 2
      } else {
        this.gridNum = this.gridNum * 2
      }
    },
    handleGridDivide: function () {
      if (!this.gridNum || this.gridNum === 0 || this.gridNum === 2) {
        return
      }
      this.gridNum = this.gridNum / 2
    },
    handelLayerChange(val) {
      this.activeTab = this.layerActiveMap[val]
       console.log(val)
    },
    handleGridChange(value) {
      console.log(value)
    },
    handleTreeVis() {
      console.log(111)
    },
    handleDrawer(val){
      this.pointDrawer = true;
      console.log(val);
      this.$refs.pointToolBar.setDrawer(this.pointDrawer);
    },

  },
  mounted: function () {
    //todo init p2
  },
})
</script>

<style>
.el-container {
  height: 100%;
}


</style>
