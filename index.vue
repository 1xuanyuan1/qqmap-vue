<template>
  <div class="map">
    <iframe id="mapPage" width="100%" height="100%" frameborder=0 
        src="http://apis.map.qq.com/tools/locpicker?search=1&type=1&key=QTVBZ-U7KR6-7UOSQ-MVPCC-F2BB2-HSFEA&referer=myapp">
    </iframe>
  </div>
</template>
<script>
export default {
  name: 'QQMap',
  methods: {
    messageListener (event) {
      // 接收位置信息，用户选择确认位置点后选点组件会触发该事件，回传用户的位置信息
      var loc = event.data
      if (loc && loc.module === 'locationPicker') { // 防止其他应用也会向该页面post信息，需判断module是否为'locationPicker'
        // console.log('location', loc)
        this.$emit('location', loc)
      }
    }
  },
  mounted () {
    window.addEventListener('message', this.messageListener, false)
  },
  destroyed () {
    window.removeEventListener('message', this.messageListener)
  }
}
</script>
<style scoped>
.map{
  width: 400px;
  height: 600px;
  overflow: hidden;
}
</style>
