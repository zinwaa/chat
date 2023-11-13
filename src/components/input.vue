<template>
    <div class="inputBox">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#fff"
            stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <polygon points="14 2 18 6 7 17 3 17 3 13 14 2"></polygon>
            <line x1="3" y1="22" x2="21" y2="22"></line>
        </svg>
        <input type="text" v-model="message" :disabled="!props.isInput">
        <button @click="seed" :disabled="!props.isInput">
            <span>seed</span>
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="#000000"
                stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <circle cx="11" cy="11" r="8"></circle>
                <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
            </svg>
        </button>
    </div>
</template>


<script setup>
var message = ''
const emits = defineEmits(['seed'])
const props = defineProps(['isInput'])
const seed = () => {
    emits('seed', message)
}
</script>


<style scoped>
.inputBox {
    position: fixed;
    bottom: 0px;
    display: flex;
    width: calc(100% - 20vh);
    border: none;
    background-color: var(--userBac);
    padding: 10px 10vh;
    height: 3vh;
    border-radius: 3vh;
    box-shadow: 2px 1px 8px 1px var(--shadow);
    justify-content: center
}

.inputBox svg {
    width: 2vh;
}

.inputBox input {
    margin-left: 10px;
    border: none;
    border-radius: .5vh 0 0 .5vh;
    flex: 1;
    padding: 2px 10px;
}

.inputBox input:focus-visible {
    outline: none;
}

.inputBox button {
    padding: 0;
    margin: 0;
    border: none;
    background: none;
    height: 100%;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
    color: #fff;
    transition: all .3s;
    border-radius: 0 .5vh .5vh 0;
    cursor: pointer;
}

.inputBox button:hover {
    background: white;
    color: var(--userBac);
}

.inputBox span {
    position: relative;
    bottom: 0.6vh;
    margin-right: 1vw;
    font-weight: 600;
    font-size: 1rem;
}

button svg {
    stroke: #fff;
    transition: all .3s;
    position: relative;
    top: 2px;
}

button:hover svg {
    stroke: var(--userBac);
}
input[disabled]{
    cursor: not-allowed;
}
button[disabled]{
    cursor: not-allowed;
    background-color: #efefef4d;
}
button[disabled]:hover{
    cursor: not-allowed;
    background-color: #efefef4d;
}
@media(max-width: 768px) {
    .inputBox {
        width: calc(100% - 10vh);
        padding: 10px 5vh;
    }
}
</style>