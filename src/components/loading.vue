<template>
    <div class="loadingBox">
        <svg class="loading" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="#00AAFF" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21.5 2v6h-6M2.5 22v-6h6M2 11.5a10 10 0 0 1 18.8-4.3M22 12.5a10 10 0 0 1-18.8 4.2" />
        </svg>
    </div>
</template>


<script setup>

</script>


<style scoped>
.loadingBox {
    line-height: 100%;
    width: 100%;
    padding-top: 10px;
    padding-bottom: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.loading {
    display: inline;
    animation: revolve 1.5s linear infinite;
    opacity: 0.7;
    transform: scale(0.9);
}

@keyframes revolve {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>