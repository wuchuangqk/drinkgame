<script setup lang="ts">
import { onLaunch, onShow, onHide } from "@dcloudio/uni-app";
onLaunch(() => {
  console.log("App Launch");
});
onShow(() => {
  console.log("App Show");
});
onHide(() => {
  console.log("App Hide");
});
</script>
<style>
/*每个页面公共css */
@import './styles/common.scss';

page {
  box-sizing: border-box;
}

:not(not) {
  box-sizing: border-box;
}
</style>
