<template>
  <div class="userChatBox">
    <div class="userBox">
      <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path><circle cx="12" cy="7" r="4"></circle></svg>
    <span>You</span>
    </div>
    <div class="chatBox">
        <slot>
        </slot>
    </div>
  </div>
</template>


<script setup>
</script>



<style scoped>
.userChatBox {
  border: 1px solid #ccc;
  width: 70vw;
  float: right;
  display: flex;
  flex-direction: column;
  border-radius: 1vw;
  margin-bottom: 3vh;
  box-shadow: 2px 1px 8px 1px var(--shadow);
}
.userBox{
  border-radius: 1vw 1vw 0 0;
  padding: 10px;
  padding-left: 2vw;
  background-color: var(--userBac);
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
}
</style>