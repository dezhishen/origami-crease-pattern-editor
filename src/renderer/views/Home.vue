<template>
  <div style="height:100%;">
    <el-container>
      <el-container>
        <el-aside style="width:270px;border:2px solid silver;height:100%;">
          <div style="height:35%;">
            <div style="height:auto;background-color: rgba(49, 110, 175, 0.95);">
             <span style="margin-left:10px;color: white;">图层控制</span>
            </div>
            <el-tree
              :data="treeData"
              show-checkbox
              default-expand-all
              :default-checked-keys = "[1,2,3,4,5,6]"
              node-key="id"
              ref="tree"
              highlight-current
              :props="defaultProps">
              <span class="custom-tree-node" slot-scope="{ node,data }">
                <span style="margin-left:5px"> 
                  <i :class="data.icon"></i>{{ node.label }}
                </span>              
              </span>
            </el-tree>
          </div>
          <div style="height:65%;"> 
            <el-tabs type="border-card" style="height:100%;">
              <el-tab-pane label="点编辑">
                <el-switch
                  v-model="addPoint"
                  active-text=""
                  inactive-text="添加点">
                </el-switch>

                <el-switch
                  v-model="delPoint"
                  active-text=""
                  inactive-text="删除点"
                  style="padding-left:30px;">
                </el-switch>

              </el-tab-pane>
              <el-tab-pane label="线编辑">  
                <el-switch
                  v-model="addLine"
                  active-text=""
                  inactive-text="添加线">
                </el-switch>

                <el-switch
                  v-model="delLine"
                  active-text=""
                  inactive-text="删除线"
                  style="padding-left:30px;">
                </el-switch>
              </el-tab-pane>
              <el-tab-pane label="网格编辑">
              <el-form  class="demo-form-inline" style="padding-left:10px;">
                <el-form-item label="设置等分数" >
                  <el-input-number v-model="gridNum" controls-position="right" @change="handleGridChange" :min="0" :max="256" size="small"></el-input-number>
                </el-form-item>
                <el-form-item>
                  <el-button-group>
                    <el-button type="primary" >X2</el-button>
                    <el-button type="primary" >X1/2</el-button>
                    <el-button type="primary" icon="el-icon-delete">归零</el-button>
                  </el-button-group>
                </el-form-item>
              </el-form>
                
              </el-tab-pane>
              <el-tab-pane label="画布工具">比如 撤销 重做 平移 缩放 旋转</el-tab-pane>
              <el-tab-pane label="选择工具">支持点选 框选 然后操作选中要素</el-tab-pane>
            </el-tabs>
          </div>
        </el-aside>
        <el-main style="background-color:#f3f3f3">
          我是画布
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'Home',
  data: function () {
    
    const treeData =  [{
          id: 1,
          label: '画布图层',
          icon: 'node_layer',
          children: [
            {
              id: 2,
              label: '网格',
              icon: 'node_grid',
            },
            {
              id: 3,
              label: '节点',
              icon: 'node_vertex',
            }, 
            {
              id: 4,
              label: '山线',
              icon: 'node_m',
            }, 
            {
              id: 5,
              label: '谷线',
              icon: 'node_v',
            }, 
            {
              id:6,
              label: '辅助线',
              icon: 'node_a',
            }
          ]
        }]
    return { 
      title: '~',
      treeData: treeData,
      gridNum: 0,
        defaultProps: {
          children: 'children',
          label: 'label',
        },
        addPoint:false,
        delPoint:false,
        addLine:false,
        delLine:false,
      }
  },
  methods:{
     handleGridChange(value: any) {
        console.log(value);
      }
  },
  mounted:function(){
    //todo init p2
  }
})
</script>

<style>
.el-container{
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



</style>
