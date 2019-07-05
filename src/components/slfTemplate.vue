<template>
  <div class="slf-template">
    <div class="frame" ref="frame">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: 'slfTemplate'
}
</script>

<style>
  .frame {
    height: auto;
    width: auto;
    border: 1px solid black;
    display: grid;
    grid-template-columns: auto repeat(4, minmax(75px, auto));
  }

  .field {
    height: 25px;
    width: 100%;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  span {
    margin: 0 5px;
  }
</style>
