<template>
    <div  class="checkbox-container" @click="click">
      <div :class="['checkbox-outer', active]">
          <div class="check-sign"></div>
      </div>
      <input type="checkbox" class="checkbox" />
      <span :class="['checkbox-text', active]">
          <slot/>
      </span>  
    </div>
</template>
<script>
import {computed, inject} from 'vue'
export default {
    props: {
        modelValue: [String, Number],
        value: [String, Number]
    },
    emits: ['update:modelValue'],
    setup(props, ctx) {
        let {isCheckboxGroup, listValue, updateModelVaule} = inject('checkList')
        console.log(isCheckboxGroup, listValue)
        function click() {
            if(isCheckboxGroup) {
                updateModelVaule(props.value)
            } else {
                ctx.emit('update:modelValue', !props.modelValue)
            }
        }
        const active = computed(()=> { 
            let currentModelValue = props.modelValue
            if(isCheckboxGroup) {
                return listValue.includes(props.value) ? 'active' : ''
            }
            return currentModelValue ? 'active' : ''
        })
        return {
            active,
            click
        }
    },
}
</script>
<style lang="scss">
@import '../style/common.scss';
.checkbox-container{
    cursor: pointer;
    display: inline-flex;
    justify-content: center;
    align-items: center;
    height: $common-height;
    margin-left: 4px;
    .checkbox{
        display: none;
    }
}
.checkbox-outer{
    width: 16px;
    height: 16px;
    border: 1px solid $border-color;
    overflow: hidden;
    transition: .3s all;
    .check-sign{
        width: 5px;
        height: 8px;
        border: 2px solid #fff;
        border-radius: 2px;
        border-top-width: 0px;
        border-left-width: 0px;
        transform: rotate(45deg) translateY(-3px) translateX(4px) scale(1);
        transition: transform 0.3s, opacity .3s, color 0.3s, border-color 0.3s;
        &:active{
            transform: scale(0);
            opacity: 0.2;
            transition: 0s;
        }
    }
}
.checkbox-container:hover .checkbox-outer{
     border: 1px solid $theme-color;
}
.checkbox-outer.active {
    background: $theme-color;
    border: 1px solid $theme-color;  
}
// .checkbox-text.active{
//     color: $theme-color;
// }
.checkbox-text{ 
    margin-left: 4px;
}
</style>