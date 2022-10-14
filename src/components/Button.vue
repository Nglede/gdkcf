<template>
  <div class="button">
    <span></span>
    <span></span>
    <span></span>
    <span></span>
    <slot></slot>
  </div>
</template>

<script setup lang="ts">

</script>

<style scoped>
.button {
  position: relative;
  padding: 0.2rem 1rem;
  height: 2rem;
  line-height: 2rem;
  color: #03e9f4;
  cursor: pointer;
  overflow: hidden;
  transition: 0.5s;
  text-align: center;
  font-weight: 600;
  letter-spacing: 4px;
}
.button:hover {
  background: #03e9f4;
  color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 5px #03e9f4, 0 0 25px #03e9f4, 0 0 50px #03e9f4,
    0 0 100px #03e9f4;
}

span {
  position: absolute;
  display: block;
}

.button span:nth-child(1) {
  top: 0;
  left: -100%;
  width: 100%;
  height: 1px;
  background: linear-gradient(90deg, transparent, #03e9f4);
  animation: btn-anim1 1s linear infinite;
}

@keyframes btn-anim1 {
  0% {
    left: -100%;
  }

  50%,
  100% {
    left: 100%;
  }
}

.button span:nth-child(2) {
  top: -100%;
  right: 0;
  width: 1px;
  height: 100%;
  background: linear-gradient(180deg, transparent, #03e9f4);
  animation: btn-anim2 1s linear infinite;
  animation-delay: 0.25s;
}

@keyframes btn-anim2 {
  0% {
    top: -100%;
  }

  50%,
  100% {
    top: 100%;
  }
}

.button span:nth-child(3) {
  bottom: 0;
  right: -100%;
  width: 100%;
  height: 1px;
  background: linear-gradient(270deg, transparent, #03e9f4);
  animation: btn-anim3 1s linear infinite;
  animation-delay: 0.5s;
}

@keyframes btn-anim3 {
  0% {
    right: -100%;
  }

  50%,
  100% {
    right: 100%;
  }
}

.button span:nth-child(4) {
  bottom: -100%;
  left: 0;
  width: 1px;
  height: 100%;
  background: linear-gradient(360deg, transparent, #03e9f4);
  animation: btn-anim4 1s linear infinite;
  animation-delay: 0.75s;
}

@keyframes btn-anim4 {
  0% {
    bottom: -100%;
  }

  50%,
  100% {
    bottom: 100%;
  }
}
</style>
