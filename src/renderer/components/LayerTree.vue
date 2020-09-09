<template>
    <el-tree
    :data= treeData
        default-expand-all
        node-key="id"
        ref="tree"
        show-checkbox
        :default-checked-keys = "[1,2,3,4,5,6]"
        :highlight-current = true
        :props="defaultProps"
        >
        <template class="custom-tree-node" slot-scope="{ node,data }">
    
        <span
            @click="handleLayerClick(node,data)"
            :label="data.id">
            <i :class="data.icon"></i>
                {{node.label}}
        </span >
    </template>
    </el-tree>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({

  data: function () {
    let treeData = [{
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
            }]
    return {
        treeData:treeData
    }
  },
  methods: {
    handleLayerClick(node,data) {
      console.log(node.label)
      console.log(data.id)
    },
  },
  mounted: function () {
    
  },
})
</script>

<style>

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