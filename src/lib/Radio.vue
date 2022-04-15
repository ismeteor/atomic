<template>
    <div class="radio-container" @click="click">
        <span :class="['radio-outer', active]">
            <span :class="['radio-inner', active]"></span>
        </span>
        <span class="radio-text"><slot/></span>
        <input class="radio" :value="modelValue" type="radio"/> 
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
        let { isRadioGroup, updateModelValue } = inject('radioGroup')
        let value = inject('value')
        function click() {
            isRadioGroup ? updateModelValue(props.value) : ctx.emit('update:modelValue', props.value)
        }
        const active = computed(()=> { 
            let currentModelValue = props.modelValue
            if( isRadioGroup ){
                currentModelValue = value.value 
            }
            return props.value == currentModelValue ? 'active' : ''
        })
        return {
            click,
            active
        }
    },
}
</script>

<style lang="scss" scoped>
@import '../style/common.scss';
.radio-container{
    display: inline-block;
    overflow: hidden;
    cursor: pointer;
    display: inline-flex;
    // padding-top: 4px;
    justify-content: center;
    align-items: center;
    height: $common-height;
}
.radio {
    display: none;
}
.radio-outer{
    width: 16px;
    height: 16px;
    border: 1px solid $border-color;
    display: inline-block;
    border-radius: 50%;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    .radio-inner{
        width: 10px;
        height: 10px;
        position: absolute;
        left: 3px;
        top: 3px;
        display: inline-block;
        border-radius: 50%;
        background: $theme-color;
        transition: transform 0.3s, opacity .3s, color 0.3s, border-color 0.3s;
        transform: scale(1);
        opacity: 0;
        &:active{
            transform: scale(0);
            opacity: 0.2;
            transition: 0s;
        }
    }
    .active {
        opacity: 1;
    }
    &.active{
        border-color: $theme-color;
    }
}
.radio-text{
    margin-left: 4px;
    line-height: 16px;
    display: inline-block;
}
</style>