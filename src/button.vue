<template>
    <button class="g-button" :class="{[`icon-${iconPosition}`]:true}" @click="$emit('update:loading',!loading)">
      <g-icon v-if="loading " class="loading" name="loading"></g-icon>
      <g-icon v-if="icon && !loading" class="icon" :name="icon"></g-icon>
      <div class="content">
        <slot/>
      </div>
    </button>
</template>
<script>

export default {
  props: {
    icon:String,
    iconPosition:{
      type:String,
      default:'left',
      validator(value) {
     return value === 'left' || value === 'right'
      }
    },
    loading:{
      type:Boolean,
      default: false
    }
  },

}
</script>
<style lang="scss">
.g-button {
  font-size: var(--font-size);height: var(--button-height);padding: 0 1em;border-radius: var(--border-radius);
  border: 1px solid var(--border-color);background: var(--button-bg);display:inline-flex;justify-content: center;
  align-items: center;vertical-align: middle;
  &:hover {border-color: var(--border-color-hover);}
  &:active {background-color: var(--button-active-bg);}
  &:focus {outline: none;}
  > .icon {order: 1;margin-right: 0.5em;margin-left: 0;}
  > .content {order: 2}
  &.icon-right {
    > .icon {order: 2;margin-right: 0;margin-left: 0.5em;}
    > .content {order: 1;} }
  .loading{
    animation: spin 2s infinite linear;
  }
  @keyframes spin {
    0% {transform: rotate(0)}
    100% {transform: rotate(360deg)}
  }
}
</style>