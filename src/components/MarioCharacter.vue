<template>
    <div ref="characterRef" class="character" :class="{characterAnimation: start}">
        <div class="character__wrapper">
            <div class="character__hat"></div>
            <div class="character__face">
                <span class="character__eye"></span>
                <span class="character__nose"></span>
                <span class="character__mustache"></span>
            </div>
            <div class="character__body">
                <span class="character__arm character__arm--left"></span>
                <span class="character__arm character__arm--right"></span>
                <span class="character__leg character__leg--left"></span>
                <span class="character__leg character__leg--right"></span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'MarioCharacter',
  props: {
    start: Boolean,
  },
  data() {
      return {
          xCorCurrent: 0,
          xCorChanged: 0,
      }
  },
  methods: {
      init() {
        let cssProps = document.querySelector(':root');
        cssProps.style.setProperty('--y-cor', 0);
        cssProps.style.setProperty('--x-cor-changed', 0);
        this.$refs.characterRef.classList.remove('characterAnimation');
        this.$refs.characterRef.classList.add('character__init');
        window.addEventListener('keydown', (e) => {
            console.log(e.key);
            switch(e.key) {
                case 'ArrowUp':
                    this.$refs.characterRef.classList.add('character__jump');
                    cssProps.style.setProperty('--y-cor', -150 + '%');
                    setTimeout(() => {
                        this.$refs.characterRef.classList.remove('character__jump');
                        cssProps.style.setProperty('--y-cor', 0);
                    }, 300);
                    break;
                case 'ArrowRight':
                    this.$refs.characterRef.classList.add('character__forward');
                    this.xCorChanged += 5;
                    cssProps.style.setProperty('--char-direction', 0);
                    cssProps.style.setProperty('--x-cor-changed', this.xCorChanged + 'vw');
                    setTimeout(() => {
                        this.$refs.characterRef.classList.remove('character__forward');
                        cssProps.style.setProperty('--x-cor-current', this.xCorChanged + 'vw');
                    }, 300);
                    break;
                case 'ArrowLeft':
                    this.$refs.characterRef.classList.add('character__forward');
                    this.xCorChanged -= 5;
                    cssProps.style.setProperty('--char-direction', -180 + 'deg');
                    cssProps.style.setProperty('--x-cor-changed', this.xCorChanged + 'vw');
                    setTimeout(() => {
                        this.$refs.characterRef.classList.remove('character__forward');
                        cssProps.style.setProperty('--x-cor-current', this.xCorChanged + 'vw');
                    }, 300);
                    break;
                default:
            }
        });
      }
  },
  watch: { 
    start:function() {
        setTimeout(() => {
            this.init();
        }, 4000);
    }
  }
}
</script>
<style scoped>
    :root {
        --x-cor-changed: 0%;
        --x-cor-current: 0%;
        --y-cor: 0%;
        --char-direction: 0;
    }

    .character {
        position: absolute;
        top: 67%;
        left: 35px;
    }

    .character__wrapper {
        position: relative;
        z-index: 100;
    }

    .character__hat {
        position: relative;
        z-index: 1;
    }

    .character__hat::before {
        content: '';
        display: block;
        width: 30px;
        height: 12px;
        background-color: #03ad03;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
    }

    .character__hat::after {
        content: '';
        display: block;
        width: 40px;
        height: 6px;
        background-color: #03ad03;
        border-top-right-radius: 8px;
    }

    .character__face {
        position: relative;
        width: 31px;
        height: 18px;
        background-color: #cf6e00;
    }

    
    .character__face::before {
        content: '';
        display: block;
        position: absolute;
        top: 0px;
        left: 7px;
        width: 12px;
        height: 11px;
        background-color: #0f018a;   
    }

    .character__face::after {
        content: '';
        display: block;
        position: absolute;
        top: -2px;
        left: -4px;
        width: 13px;
        border-top-left-radius: 8px;
        height: 20px;
        background-color: #0f018a;   
    }

    .character__eye {
        position: absolute;
        z-index: 2;
        right: 3px;
        top: 3px;
        width: 4px;
        height: 4px;
        background-color: #0f018a;   
        border-radius: 50%;
    }

    .character__nose {
        position: absolute;
        right: -5px;
        top: 3px;
        width: 10px;
        height: 8px;
        transform: rotate(51deg);
        background-color: #cf6e00;
    }

    .character__mustache {
        position: absolute;
        right: -2px;
        top: 10px;
        width: 10px;
        height: 4px;
        background-color: #0f018a;
        border-top-left-radius: 8px;
    }

    .character__body {
        position: relative;
        width: 25px;
        height: 24px;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
        background-color: #03ad03;
    }

    .character__arm {
        position: absolute;
        width: 8px;
        height: 26px;
        left: 10px;
        top: 4px;
        background-color: #0f018a;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
    }

    .character__arm::after {
        content: '';
        display: block;
        position: absolute;
        width: 8px;
        height: 6px;
        left: 0;
        bottom: -4px;
        background-color: #fff;
        border-bottom-left-radius: 8px;
        border-bottom-right-radius: 8px;
    }

    .character__arm--left {
        transform: rotate(-30deg);
    }

    .character__arm--right {
        transform: rotate(40deg);
        left: 4px;
        z-index: -1;
    }

    .character__leg {
        position: absolute;
        width: 12px;
        height: 26px;
        left: 4px;
        z-index: -1;
        bottom: -17px;
        background-color: #03ad03;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
    }

    .character__leg::after {
        content: '';
        display: block;
        position: absolute;
        width: 16px;
        height: 8px;
        left: 0;
        bottom: -6px;
        background-color: #964B00;
        border-top-right-radius: 8px;
    }

    .characterAnimation {
        animation: mario-walk 4s forwards;
    }

    .characterAnimation .character__arm--left {
        left: 6px;
        animation: arm-move 0.6s infinite;
    }

    .characterAnimation .character__arm--right {
        animation: arm-move-right 0.6s infinite;
    }

    .characterAnimation .character__leg--left {
        animation: leg-move 0.6s infinite;
    }

    .characterAnimation .character__leg--right {
        animation: leg-move-right 0.6s infinite;
    }

    /*character states*/
    .character__init {
        /*transform: translateY(0) !important;*/
        transform: translate(var(--x-cor-changed), var(--y-cor)) rotateY(var(--char-direction))!important;
    }

    .character__jump {
        animation: jump 300ms linear;
    }

    .character__jump .character__arm--left {
        transform: rotate(-80deg);
        transform-origin: center top;
    }

    .character__jump .character__arm--right {
        transform: rotate(30deg);
        transform-origin: center top;
    }

    .character__jump .character__leg--left {
        transform: rotate(-25deg);
        transform-origin: center top;
    }

    .character__jump .character__leg--right {
        transform: rotate(25deg);
        transform-origin: center top;
    }

    .character__forward {
        animation: forward 300ms linear;
    }

    .character__forward .character__leg--left {
        transform: rotate(-25deg);
        transform-origin: center top;
    }

    .character__forward .character__leg--right {
        transform: rotate(25deg);
        transform-origin: center top;
    }

    @keyframes jump {
        0% { transform: translate(var(--x-cor-changed), 0%) rotateY(var(--char-direction)); }
        50% { transform: translate(var(--x-cor-changed), var(--y-cor))rotateY(var(--char-direction)); }
        100% { transform: translate(var(--x-cor-changed), 0%) rotateY(var(--char-direction)); }
    }

    @keyframes forward {
        0% { transform: translate(var(--x-cor-current), var(--y-cor)) rotateY(var(--char-direction)); }
        100% { transform: translate(var(--x-cor-changed), var(--y-cor)) rotateY(var(--char-direction)); }
    }

    @keyframes mario-walk {
        0% {
            transform: translateX(0);
        }

        10% {
            transform: translateX(9vw);
        }
        
        20% {
            transform: translateX(18vw);
        }

        30% {
            transform: translateX(27vw);
        }

        40% {
            transform: translateX(36vw);
        }
    
        50% {
            transform: translateX(45vw) translateY(-50px);
        }

        60% {
            transform: translateX(54vw) translateY(0);
        }

        70% {
            transform: translateX(63vw);
        }

        80% {
            transform: translateX(72vw);
        }

        90% {
            transform: translateX(81vw);
        }

        95% {
            transform: translateX(90vw);
        }
    
        100% {
            transform: translateX(100vw);
        }
    }

    @keyframes arm-move {
       0% {
            transform: rotate(0deg);
            transform-origin: center top;
        }

        40% {
            transform: rotate(-80deg);
            transform-origin: center top;
        }

        80% {
            transform: rotate(0deg);
            transform-origin: center top;
        }

        100% {
            transform: rotate(30deg);
            transform-origin: center top;
        }
    }

    @keyframes arm-move-right {
        0% {
            transform: rotate(0deg);
            transform-origin: center top;
        }

        40% {
            transform: rotate(30deg);
            transform-origin: center top;
        }

        80% {
            transform: rotate(0deg);
            transform-origin: center top;
        }

        100% {
            transform: rotate(-80deg);
            transform-origin: center top;
        }
    }

    @keyframes leg-move {
        0% {
            transform: rotate(30deg);
            transform-origin: center top;
        }

        50% {
            transform: rotate(-25deg);
            transform-origin: center top;
        }

        100% {
            transform: rotate(-50deg);
            transform-origin: center top;
        }
    }

    @keyframes leg-move-right {
        0% {
            transform: rotate(-50deg);
            transform-origin: center top;
        }

        50% {
            transform: rotate(-25deg);
            transform-origin: center top;
        }

        100% {
            transform: rotate(30deg);
            transform-origin: center top;
        }
    }
</style>