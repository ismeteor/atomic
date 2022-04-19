<template>
    <div class="check-group">
        <slot/>
    </div>
</template>
<script>
import {reactive, provide, watch, computed, nextTick} from 'vue'
export default {
    props: {
        modelValue: {
            type: Array,
            default: () => []
        },
        value: [String, Number]
    },
    emits: ['update:modelValue','change', 'changeList'],
    setup(props, {emit}) {
         const changeEvent = (value) => {
            emit('update:modelValue', value)
            nextTick(() => {
                emit('change', value)
            })
        }

        let modelValue = computed({
            get() {
                return props.modelValue
            },
            set(val) {
                changeEvent(val)
            }
        })
        provide('checkList', {
           listValue: modelValue,
           isCheckboxGroup: true,
           updateModelVaule: changeEvent
        })
        
        watch(
            () => props.modelValue
        )
    },
}
</script>
<style lang="scss">
@import '../style/common.scss';

</style>