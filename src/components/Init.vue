<template>
  <div class="modal is-active">
    <div class="modal-background"></div>
    <div class="modal-content loader">
    <div class="lds-roller">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>
    </div>
  </div>
</template>

<script>
import db from '@/db'
import router from '@/router'

function generateId(length) {
  let id = ''
  const consonants = 'BCDFGHKLMNPRSTVWXZbcdfghklmnpqrstvwxz'
  const vovels = 'aeiouy'
  for (var i = 0; i < length; i++) {
    if (i % 2 === 0) {
      id += consonants.charAt(Math.floor(Math.random() * consonants.length))
    } else {
      id += vovels.charAt(Math.floor(Math.random() * vovels.length))
    }
  }
  return id
}

function findStorageId() {
  let id = generateId(6)
  db.ref(id).once('value', storage => {
    if (storage.val() === null) {
      localStorage.setItem('storageId', id)
      router.push('/')
    } else {
      setTimeout(findStorageId, 0)
    }
  })
}

export default {
  created() {
    if (localStorage.getItem('storageId') !== null) {
      router.push('/')
    } else {

      findStorageId()
    }
  }
}
</script>

<style scoped>
.modal-content.loader{
  width: 128px;
  height:  128px;
  overflow: hidden;
}
.lds-roller {
  display: inline-block;
  position: relative;
  width: 128px;
  height: 128   px;
}
.lds-roller div {
  animation: lds-roller 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 32px 32px;
}
.lds-roller div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #fff;
  margin: -3px 0 0 -3px;
}
.lds-roller div:nth-child(1) {
  animation-delay: -0.036s;
}
.lds-roller div:nth-child(1):after {
  top: 50px;
  left: 50px;
}
.lds-roller div:nth-child(2) {
  animation-delay: -0.072s;
}
.lds-roller div:nth-child(2):after {
  top: 54px;
  left: 45px;
}
.lds-roller div:nth-child(3) {
  animation-delay: -0.108s;
}
.lds-roller div:nth-child(3):after {
  top: 57px;
  left: 39px;
}
.lds-roller div:nth-child(4) {
  animation-delay: -0.144s;
}
.lds-roller div:nth-child(4):after {
  top: 58px;
  left: 32px;
}
.lds-roller div:nth-child(5) {
  animation-delay: -0.18s;
}
.lds-roller div:nth-child(5):after {
  top: 57px;
  left: 25px;
}
.lds-roller div:nth-child(6) {
  animation-delay: -0.216s;
}
.lds-roller div:nth-child(6):after {
  top: 54px;
  left: 19px;
}
.lds-roller div:nth-child(7) {
  animation-delay: -0.252s;
}
.lds-roller div:nth-child(7):after {
  top: 50px;
  left: 14px;
}
.lds-roller div:nth-child(8) {
  animation-delay: -0.288s;
}
.lds-roller div:nth-child(8):after {
  top: 45px;
  left: 10px;
}
@keyframes lds-roller {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
