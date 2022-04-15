<template>
    <div class="radio-group">
        {{modelValue}}
        <slot/>
    </div>
</template>
<script>
import {provide, reactive, watchEffect, ref } from 'vue'
export default {
    props: {
        modelValue: [String, Number]
    },
    emits: ['update:modelValue'],
    setup(props, ctx) {
        let value = ref(1)
        const updateVal = (val) => {
            value.value = val
        }
        let radioGroup = reactive({
            isRadioGroup: true,
            updateModelValue: (val)=>{
                ctx.emit('update:modelValue', val)
                updateVal(val)
            }
        })

        provide('radioGroup', radioGroup)
        provide('value', value)    
        watchEffect(() => {
            value.value = props.modelValue
        })
    },
}
</script>

<style lang="scss" scoped>
@import '../style/common.scss';
.radio-group {
    display: inline-flex;
    height: $common-height;
    justify-content: center;
}
</style>