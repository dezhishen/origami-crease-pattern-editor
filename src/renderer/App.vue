<template>
  <div id="app" class="container-fluid">
    <Transition mode="out-in" name="slide-up">
      <!-- <keep-alive> -->
      <RouterView />
      <!-- </keep-alive> -->
    </Transition>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'ImageParsing',
})
</script>

<style lang="scss">
@font-face {
  font-family: BlinkMacSystemFont,-apple-system,"Segoe UI";
  src: url("./assets/style/element-ui/theme/fonts/Segoe-UI.ttf") format("ttf");
}
button, input, select, textarea ,span , div{
    font-family: BlinkMacSystemFont,-apple-system,"Segoe UI";
    font-size: inherit;
    line-height: inherit;
    color: inherit;
}
html{
  height: 100%;
}
body {
  height: 100%;
  padding: 2px;
}
.container-fluid {
  height:100%
}
</style>
