<template>
    <div class="check-group">
        <slot/>
    </div>
</template>
<script>
import {reactive, provide, watchEffect} from 'vue'
export default {
    props: {
        modelValue: {
            type: Array,
            default: () => []
        },
        value: [String, Number]
    },
    emits: ['update:modelValue'],
    setup(props, ctx) {
        let list = reactive(props.modelValue)
        provide('checkList', {
           listValue: props.modelValue,
           isCheckboxGroup: true,
           updateModelVaule(val) {
               if(list.includes(val)) {
                   // eslint-disable-next-line vue/no-mutating-props
                   list.splice(list.indexOf(val), 1)
               } else {
                   // eslint-disable-next-line vue/no-mutating-props
                   list.push(val)
               }
               console.log(val, list)
            //    ctx.emit('update:modelValue', props.modelValue)
           }
        })
        
    },
}
</script>
<style lang="scss">
@import '../style/common.scss';

</style>