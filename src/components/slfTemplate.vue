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
    grid-template-columns: auto repeat(3, minmax(75px, auto)) auto;
  }

  .field {
    height: 25px;
    width: 100%;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .field:focus {
    outline: none;
  }

  span {
    margin: 0 5px;
  }
</style>
