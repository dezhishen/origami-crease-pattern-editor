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

    primeRect(){
        return new fabric.Rect({
            top : 25,
            left : 100,
            width : 300,
            height : 300,
            fill : 'white',
            stroke:'black',
            transparentCorners: true,
            hasControls:false,
            strokeWidth: 1,
        });
    },


    renderCanvas:function(init,ptr){
        let canvas = undefined;
        if(ptr.fCanvas === undefined){
            canvas = ptr.canvas(ptr);
        }else{
            canvas = ptr.fCanvas;
        } 

        let rect = undefined;
        if(ptr.pRect === undefined){
            rect = ptr.primeRect();
        }else{
            rect = ptr.pRect;
        }
        
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
    that.renderCanvas(true,that);
    window.addEventListener("resize", () => {
        
        setTimeout(function() {
            console.log(that);
            that.renderCanvas(false,that);
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