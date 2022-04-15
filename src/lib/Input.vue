<template>
    <div class="input-outer">
       <input :value="val" @input="setVal" type="text">
    </div>
</template>
<script>
import { ref } from 'vue'
export default {
    props: {modelValue: String},
    emits: ['update:modelValue'],
    setup(props, ctx) {
        const val = ref(props.modelValue)
        const setVal = (event) => {
            val.value = event.target.value
            ctx.emit('update:modelValue', val.value)
        }
        return {
            val,
            setVal
        }
    },
}
</script>
<style lang="scss" scoped>
@import '../style/common.scss';
.input-outer {
    height: $common-height;
    input {
        box-sizing: border-box;
        width: 100%;
        height: 100%;
        border-radius: $border-radius;
        border: 1px solid #ccc;
        font-size: 16px;
    }
    input:focus{
        border: 1px solid white;
        // border: 0;
        outline: 1px solid skyblue;
    }
}
</style>