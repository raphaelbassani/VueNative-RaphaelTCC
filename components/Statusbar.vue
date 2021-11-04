<template>
  <view class="statusbar" :style="{ backgroundColor: color }"></view>
</template>

<script>
export default {
  props: ["color"]
};
</script>

<style>
.statusbar {
  background-color: #ffffff;
  height: 40px;
}
</style>