<template>
  <div class="template">
    <div class="frame">
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
      <div class="test"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'template'
}
</script>

<style>
  .frame {
    height: 250px;
    width: 500px;
    border: 1px solid black;
    display: grid;
    grid-template-columns: 15px repeat(4, 1fr);
  }

  .test {
    height: 100%;
    width: 100%;
    border: 1px solid black;
  }
</style>
