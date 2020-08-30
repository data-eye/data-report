<template>
  <div class="home">
    <top-view />
    <reading-view />
    <bottom-view />
    <map-view />
  </div>
</template>

<script>
// @ is an alias to /src
import TopView from "../components/TopView";
import ReadingView from "../components/ReadingView";
import BottomView from "../components/BottomView";
import MapView from "../components/MapView";

export default {
  name: "Home",
  components: {
    TopView,
    ReadingView,
    BottomView,
    MapView
  }
};
</script>

<style lang="scss" scoped>
.home {
  width: 100%;
  height: 100%;
  padding: 20px;
  background-color: #eee;
  box-sizing: border-box;
}
</style>
