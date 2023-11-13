<template>
    <div class="tip" :class="props.type">
        <slot></slot>

        <!-- tip中的内容由slot提供 -->
    </div>
</template>


<script setup>
/*
 * :type,值为error / ok
 * error 为错误，ok 为正确 
 * 值不同，css不同
 * 
 * 父组件用v-show控制显示
 */
const props = defineProps(['type'])
</script>


<style scoped>
.tip {
    position: fixed;
    top: 60px;
    left: 50%;
    transform: translateX(-50%);
    transition: all 0.5s;
    background-color: #fff;
    text-align: center;
    font-size: 0.8rem;
    border-radius: 1vw;
    padding: 2.5vw;
    opacity: 0;
    animation: inout 2s linear;
}

.ok {
    border: 1px solid #00AAFF;
    box-shadow: 1px 1px 8px 1px #00AAFF;
    color: #00AAFF;
}

.error {
    border: 1px solid #ff3131;
    box-shadow: 1px 1px 8px 1px #ff3131;
    color: #ff3131;
}

@keyframes inout {

    10%,
    90% {
        transform: translate(-50%, 20px);
        opacity: 1;
    }
}</style>