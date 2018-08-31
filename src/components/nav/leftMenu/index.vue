<template>
  <div class="sidebar">
    <dl>
      <dt class="h2 mt10">菜单1</dt>
      <dt class="h2 mt10">菜单2</dt>
      <dt class="h2 mt10">菜单3</dt>
    </dl>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  }
};
</script>
<style lang="scss">
.sidebar {
  background-color: #191818;
  border-right: 1px solid #eee;
  min-height: 100%;
  dt {
    height: 60px;
    line-height: 60px;
    color: red;
    padding: 0 20px 0 47px;
    border-bottom: 1px solid #dbe1e5;
    cursor: pointer;
  }
}
</style>