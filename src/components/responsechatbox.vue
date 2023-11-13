<template>
    <div class="responseChatBox">
        <div class="userBox">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#fff"
                stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <path
                    d="M21.2 15c.7-1.2 1-2.5.7-3.9-.6-2-2.4-3.5-4.4-3.5h-1.2c-.7-3-3.2-5.2-6.2-5.6-3-.3-5.9 1.3-7.3 4-1.2 2.5-1 6.5.5 8.8M12 19.8V12M16 17l-4 4-4-4" />
            </svg>
            <span>面试展示</span>
        </div>
        <div class="chatBox">
            <slot>
                <loading />
            </slot>
        </div>
    </div>
</template>


<script setup>
import loading from './loading.vue';
</script>


<style scoped>
.responseChatBox {
    border: 1px solid #ccc;
    width: 70vw;
    float: left;
    display: flex;
    flex-direction: column;
    border-radius: 1vw;
    box-shadow: 2px 1px 8px 1px var(--shadow);
    margin-bottom: 3vh;
}

.userBox {
    border-radius: 1vw 1vw 0 0;
    padding: 10px;
    padding-left: 2vw;
    background-color: var(--response);
    height: 2vh;
}

.userBox span {
    color: #fff;
    margin-left: 10px;
    font-size: 0.85rem;
    position: relative;
    top: -0.3vh;
}

.chatBox {
    padding: 10px;
    font-size: 0.85rem;
    display: flex;
    flex-direction: column;
    gap: 3px;
}</style>