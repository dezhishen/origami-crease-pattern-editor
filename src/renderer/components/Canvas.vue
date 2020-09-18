<template>
    <el-main ref = "cc">
        <canvas  id="fcanvas"></canvas>
    </el-main>
</template>

<script>
import Vue from 'vue'
import Fabric from 'fabric'

Vue.use(Fabric);
export default Vue.extend({
  name: 'Canvas',
  data: function () {
    let fCanvas = undefined;
    let pRect = undefined;
    return {
       
    }
  },
  methods: {
    canvas(ptr){
        return new fabric.Canvas('fcanvas',{
            width:ptr.$refs.cc.$el.clientWidth,
            height: ptr.$refs.cc.$el.clientHeight,
            backgroundColor:'white',
            selection: false
        });
    },

    primeRect(sideLen){
        return new fabric.Rect({
            top : 25,
            left : 100,
            width : sideLen,
            height : sideLen,
            fill : 'white',
            stroke:'black',
            transparentCorners: true,
            hasControls:false,
            strokeWidth: 1,
        });
    },


    renderCanvas:function(init,canvas,rect){

        if(init){
            canvas.centerObject(rect);
        }else{
            canvas.remove(rect);
        }
        canvas.add(rect);
        canvas.renderAll();

    },


  },
 mounted: function () {
    const that = this
    this.fCanvas = this.canvas(this);
    
    let dWidth = this.$refs.cc.$el.clientWidth;
    let dHeight = this.$refs.cc.$el.clientHeight;

    let sideLen =  dWidth> dHeight ? 0.9 * dHeight : 0.9 * dWidth;
    this.pRect = this.primeRect(sideLen);

    this.renderCanvas(true,this.fCanvas,this.pRect);
    window.addEventListener("resize", () => {
        that.fCanvas.setWidth(that.$refs.cc.$el.clientWidth);
        that.fCanvas.setHeight(that.$refs.cc.$el.clientHeight);
        setTimeout(function() {
            that.renderCanvas(false,that.fCanvas,that.pRect);
        }, 100);
    });
  },
})
</script>
<style scoped>
    #fcanvas{
        border: 1px dashed black;
    }
</style>>