<template>
    <button class="button button-ripple">
        <slot></slot>
    </button>
</template>
<script>
export default {
    setup() {
        
    },
}
</script>
<style lang="scss" scoped>
@import '../style/common.scss';
.button {
    border: none;
    outline: none;
    padding: 4px 8px;
    background: #fff;
    border: 1px solid #ccc;
    border-radius: $border-radius;
    &:hover{
        color: $theme-color;
        border-color: $theme-color;
    }
}
.button-ripple {
  overflow: hidden;
  position: relative;
  transition: background-color 0.3s linear, border 0.3s linear;
  &:after {
    content: "";
    display: block;
    position: absolute; 
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    pointer-events: none;
    background-image: radial-gradient(
      circle,
      $theme-color 10%,
      rgba(0, 0, 0, 0) 10.01%
    );
    background-repeat: no-repeat;
    background-position: 50%;
    transform: scale(10);
    opacity: 0;
    transition: transform 0.5s, opacity 1s, color 0.3s, border-color 0.3s;
  }
  &:active:after {
    transform: scale(0);
    opacity: 0.2;
    transition: 0s;
  }
}
</style>