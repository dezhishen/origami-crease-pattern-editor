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
        let cvs = new fabric.Canvas('fcanvas',{
            width:ptr.$refs.cc.$el.clientWidth,
            height: ptr.$refs.cc.$el.clientHeight,
            backgroundColor:'white',
            selection: false
        });
        cvs.on("mouse:wheel",  function(opt) {
            var delta = opt.e.deltaY;
            var zoom = cvs.getZoom();
            zoom *= 0.999 ** delta;
            if (zoom > 20) zoom = 20;
            if (zoom < 0.01) zoom = 0.01;
            cvs.zoomToPoint({ x: opt.e.offsetX, y: opt.e.offsetY }, zoom);
            opt.e.preventDefault();
            opt.e.stopPropagation();
        });
        cvs.on('mouse:down', function(opt) {
            var evt = opt.e;
            if (evt.altKey === true) {
                this.isDragging = true;
                this.selection = false;
                this.lastPosX = evt.clientX;
                this.lastPosY = evt.clientY;
        }
        });
        cvs.on('mouse:move', function(opt) {
        if (this.isDragging) {
            var e = opt.e;
            var vpt = this.viewportTransform;
            vpt[4] += e.clientX - this.lastPosX;
            vpt[5] += e.clientY - this.lastPosY;
            this.requestRenderAll();
            this.lastPosX = e.clientX;
            this.lastPosY = e.clientY;
        }
        });
        cvs.on('mouse:up', function(opt) {
            this.setViewportTransform(this.viewportTransform);
            this.isDragging = false;
            this.selection = true;
        });
        return cvs;
    },

    primeRect(sideLen){
        let rct = new fabric.Rect({
            top : 25,
            left : 100,
            width : sideLen,
            height : sideLen,
            fill : 'white',
            stroke:'indigo',
            centeredScaling:true,
            centeredRotation:true,
            originX: 'center',
            originY: 'center', 
            transparentCorners: true,
            hasControls:false,
            strokeWidth: 1,
            evented: false,
            selectable: false ,
            
        });
        return rct;
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
        border: 1px solid silver;
    }
</style>>