<template>
  <div style="height:100%;">
    <el-container>
      <el-container>
        <el-aside style="width:270px;border:2px solid silver;height:100%;">
          <div style="height:35%;overflow:auto;">
            <div style="height:auto;background-color: rgba(49, 110, 175, 0.95);">
              <span style="margin-left:10px;color: white;">图层控制</span>
            </div>
            <el-tree
              :data="[{
                    id: 1,
                    label: '画布图层',
                    icon: 'node_layer',
                    isLeaf:false,
                    children: [
                      {
                        id: 2,
                        label: '网格',
                        icon: 'node_grid',
                        isLeaf:true
                      },
                      {
                        id: 3,
                        label: '节点',
                        icon: 'node_vertex',
                        isLeaf:true
                      },
                      {
                        id: 4,
                        label: '山线',
                        icon: 'node_m',
                        isLeaf:true
                      },
                      {
                        id: 5,
                        label: '谷线',
                        icon: 'node_v',
                      },
                      {
                        id: 6,
                        label: '辅助线',
                        icon: 'node_a',
                        isLeaf:true
                      },
                    ],
                  }]"
              default-expand-all
              node-key="id"
              ref="tree"
              highlight-current
              :props="defaultProps"
            >
              <template class="custom-tree-node" slot-scope="{ node,data }">
                <el-radio
                  v-if="node.isLeaf"
                  @change="handelLayerChange"
                  v-model="curLayerId"
                  :label="data.id"
                >
                  <i :class="data.icon"></i>
                  {{node.label}}
                </el-radio>
                <span v-else>
                  <i :class="data.icon"></i>
                  {{node.label}}
                </span>
              </template>
            </el-tree>
          </div>
          <div style="height:65%;">
            <el-tabs type="border-card" v-model="activeTab" style="height:100%;">
              <el-tab-pane v-if="curLayerId===3" name="point" label="点编辑" style="display:none;">
                <el-switch v-model="pointAction" active-text="添加点" inactive-text="删除点"></el-switch>
              </el-tab-pane>
              <el-tab-pane
                name="line"
                v-if="curLayerId===4||curLayerId===5||curLayerId===6"
                label="线编辑"
                style="display:none;"
              >
                <el-switch v-model="lineAction" active-text="添加线" inactive-text="删除线"></el-switch>
              </el-tab-pane>
              <el-tab-pane name="grid" v-if="curLayerId===2" label="网格编辑" style="display:none;">
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
              <el-tab-pane name="chooseTool" label="选择工具">支持点选 框选 然后操作选中要素</el-tab-pane>
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
        <el-main style="background-color:#f3f3f3">我是画布</el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'Home',
  data: function () {
    return {
      activeTab: 'grid',
      curLayerId: 2,
      layerActiveMap: {
        2: 'grid',
        3: 'point',
        4: 'line',
        5: 'line',
        6: 'line',
      },
      activeTabs: ['grid', 'layerTool', 'chooseTool'],
      gridNum: 0,
      defaultProps: {
        children: 'children',
        label: 'label',
        isLeaf: 'isLeaf',
      },
      pointAction: true,
      lineAction: true,
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
    },
    handleGridChange(value) {
      console.log(value)
    },
    handleTreeVis() {
      console.log(111)
    },
    handleLayerClick(node) {
      console.log(node.label)
      this.curLayerId = node.id
      if (node.id == 3) {
      }
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
.node_layer {
  padding-left: 20px;
  background: url('/static/images/layer.ico') no-repeat 0 3px;
}
.node_grid {
  padding-left: 20px;
  background: url('/static/images/grid.ico') no-repeat 0 3px;
}
.node_vertex {
  padding-left: 20px;
  background: url('/static/images/dotblack.ico') no-repeat 0 3px;
}
.node_m {
  padding-left: 20px;
  background: url('/static/images/redline.ico') no-repeat 0 3px;
}
.node_v {
  padding-left: 20px;
  background: url('/static/images/blueline.ico') no-repeat 0 3px;
}

.node_a {
  padding-left: 20px;
  background: url('/static/images/greyline.ico') no-repeat 0 3px;
}

.ptShow {
  display: inline;
}

.ptHide {
  display: none;
}
</style>
