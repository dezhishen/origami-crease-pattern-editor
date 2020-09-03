<template>
  <div style="margin-top:5px;margin-bottom:5px;height:100%">
    <el-container>
      <el-container>
        <el-aside style="width:300px;border:1px solid grey;height:100%;">
          <div style="height:60%;">
            <el-tree
              :data="treeData"
              show-checkbox
              default-expand-all
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
          <div style="height:40%;"> 
            <el-tabs type="border-card" style="height:100%;">
              <el-tab-pane label="点编辑">点编辑</el-tab-pane>
              <el-tab-pane label="线编辑">线编辑</el-tab-pane>
              <el-tab-pane label="网格编辑">网格编辑</el-tab-pane>
              <el-tab-pane label="画布工具">画布工具</el-tab-pane>
            </el-tabs>
          </div>
        </el-aside>
        <el-main>[][][]</el-main>
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
        defaultProps: {
          children: 'children',
          label: 'label',
        }
      }
  },
  methods:{

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
