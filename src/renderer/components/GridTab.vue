<template>
    <el-tab-pane name="grid"  label="网格编辑" >
        <template>
            <el-form class="demo-form-inline" style="padding-left:10px;">
                <el-form-item label="等分数">
                    <el-input-number
                    v-model="gridNum"
                    controls-position="right"
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
</template>
<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'GridTab',
  data: function () {
    return {
      gridNum: 0,
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

  },

})
</script>