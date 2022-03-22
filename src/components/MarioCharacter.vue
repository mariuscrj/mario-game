<template>
    <div class="character" :class="{characterAnimation: start}">
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
}
</script>
<style scoped>
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