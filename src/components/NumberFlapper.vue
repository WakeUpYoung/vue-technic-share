<template>
  <div>
    <div class="flapper-container text-center text-white bg-dark disable-select position-relative">
      <div :id="`flapper-top${_uid}`" class="flapper-content flapper-top position-relative" :class="flapperAni">
        <div :class="{flapping: isFlapping}">{{ numberArray[aboveIndex] }}</div>
      </div>
      <div class="flapper-content flapper-bottom">{{ numberArray[aboveIndex] }}</div>
      <div class="flapper-content flapper-rear position-absolute">{{ numberArray[rearIndex] }}</div>
    </div>
    <b-button class="mt-3" @click="click" size="sm" variant="info">CLICK ME</b-button>
  </div>
</template>

<script>
export default {
  name: 'NumberFlapper',
  data () {
    return {
      aboveNum: 3,
      rearNum: 4,
      flapperAni: '',
      numberArray: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      aboveIndex: 0,
      rearIndex: 1,
      isFlapping: false
    }
  },
  methods: {
    click () {
      if (!this.flapperAni) {
        this.flapperAni = 'rotate'
      }
    }
  },
  mounted () {
    const vm = this
    const flapperTop = document.getElementById(`flapper-top${vm._uid}`)
    flapperTop.addEventListener('animationstart', (e) => {
      console.log(e)
      setTimeout(() => {
        vm.aboveIndex = (vm.aboveIndex + 1) % 10
        vm.isFlapping = true
      }, 250)
    }, false)

    flapperTop.addEventListener('animationend', (e) => {
      console.log(e)
      vm.flapperAni = ''
      vm.rearIndex = (vm.rearIndex + 1) % 10
      vm.isFlapping = false
    }, false)
  }
}
</script>

<style scoped>
.flapper-container {
  font-size: 2rem;
  width: 3rem;
  height: 4rem;
}

.flapper-content {
  height: 2rem;
  width: 100%;
  overflow: hidden;
  background-color: #343A40;
  border-radius: 5px;
}

.flapper-content.flapper-top {
  z-index: 4;
  line-height: 3.9rem;
  transform-origin: bottom;
  animation-fill-mode: backwards;
  border-bottom-color: #f0f0f0;
  border-bottom-width: 1px;
  border-bottom-style: solid;
}

.flapper-content.flapper-top.rotate {
  animation-name: flapdown;
  animation-duration: 500ms;
}

.flapping {
  transform: rotate(0.5turn) rotateY(180deg);
  transform-origin: center;
}

.flapper-content.flapper-bottom {
  z-index: 3;
  line-height: 0;
  border-top-color: #f0f0f0;
  border-top-width: 1px;
  border-top-style: solid;
}

.flapper-content.flapper-rear {
  z-index: 2;
  top: 0;
  line-height: 3.9rem;
  border-bottom-color: #f0f0f0;
  border-bottom-width: 1px;
  border-bottom-style: solid;
}

@keyframes flapdown {
  0% {
    transform: perspective(0px) rotateX(0deg);
  }
  50% {
    transform: perspective(80px) rotateX(-90deg);
  }
  100% {
    transform: perspective(80px) rotateX(-180deg);
  }
}
</style>
