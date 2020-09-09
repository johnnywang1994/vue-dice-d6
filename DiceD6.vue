<template>
  <div class="dice-wrapper">
    <div :class="[
      'dice',
      size,
      `point${result}`,
      {[`scrolling-${scrollType}`]: start}
    ]">
      <div
        v-for="page in 6"
        :key="`dp_${page}`"
        :class="[
          'page',
          `page${page}`,
          !diceBg && 'dice-default',
        ]"
        :style="pageStyle"
      >
        <span
          v-for="span in page"
          :key="`dps_${span}`"
          :style="pointStyle"
        ></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DiceD6',
  props: {
    scrollType: {
      type: String,
      default: 'random',
      validator(value) {
        return ['random', 'round'].indexOf(value) > -1;
      },
      description: 'Dice animation type',
    },
    result: {
      type: Number,
      default: 1,
      description: 'Result Dice Point',
    },
    start: {
      type: Boolean,
      default: false,
      description: 'Whether Start Dice Animation',
    },
    diceBg: {
      type: String,
      description: 'Dice background image url',
    },
    dicePoint: {
      type: String,
      description: 'Dice point image url',
    },
    size: {
      type: String,
      default: 's',
      validator(value) {
        return ['xs', 's', 'm', 'l', 'xl'].indexOf(value) > -1;
      },
      description: 'Dice size options',
    },
  },
  computed: {
    pageStyle() {
      const vm = this;
      if (vm.diceBg) {
        return {
          background: `url('${vm.diceBg}') center / cover no-repeat`,
        };
      }
      return {};
    },
    pointStyle() {
      const vm = this;
      if (vm.dicePoint) {
        return {
          background: `url('${vm.dicePoint}') center / cover no-repeat`,
        };
      }
      return {};
    }
  }
}
</script>

<style lang="scss">
@keyframes dice-scroll-1 {
  0% {
    transform: rotateX(0deg) rotateY(0deg) rotateZ(0deg);
  }
  25% {
    transform: rotateX(0deg) rotateY(90deg) rotateZ(90deg);
  }
  50% {
    transform: rotateX(0deg) rotateY(180deg) rotateZ(180deg);
  }
  75% {
    transform: rotateX(180deg) rotateY(270deg) rotateZ(270deg);
  }
  100% {
    transform: rotateX(360deg) rotateY(360deg) rotateZ(360deg);
  }
}

@keyframes dice-scroll-2 {
  0% {
    transform: rotateX(45deg) rotateY(0deg) rotateZ(45deg);
  }
  12.5% {
    transform: rotateX(45deg) rotateY(45deg) rotateZ(0deg);
  }
  25% {
    transform: rotateX(90deg) rotateY(45deg) rotateZ(-45deg);
  }
  37.5% {
    transform: rotateX(135deg) rotateY(45deg) rotateZ(-90deg);
  }
  50% {
    transform: rotateX(135deg) rotateY(0deg) rotateZ(-135deg);
  }
  62.5% {
    transform: rotateX(135deg) rotateY(-45deg) rotateZ(-180deg);
  }
  75% {
    transform: rotateX(90deg) rotateY(-45deg) rotateZ(-225deg);
  }
  87.5% {
    transform: rotateX(45deg) rotateY(-45deg) rotateZ(-270deg);
  }
  100% {
    transform: rotateX(50deg) rotateY(0deg) rotateZ(-315deg);
  }
}

.dice-wrapper {
  perspective: 800px;
  overflow: hidden;
  .dice {
    position: relative;
    transform: rotateX(50deg) rotateY(0deg) rotateZ(-315deg);
    transition: transform 500ms; // dice scroll speed
    transform-style: preserve-3d;
    &.scrolling-random {
      animation: dice-scroll-1 1s linear infinite;
    }
    &.scrolling-round {
      animation: dice-scroll-2 0.5s linear infinite;
    }
    &.point2 {
      transform: rotateX(-45deg) rotateY(-135deg) rotateZ(-90deg);
    }
    &.point3 {
      transform: rotateX(-45deg) rotateY(315deg) rotateZ(90deg);
    }
    &.point4 {
      transform: rotateX(-45deg) rotateY(135deg) rotateZ(0deg);
    }
    &.point5 {
      transform: rotateX(135deg) rotateY(225deg) rotateZ(0deg);
    }
    &.point6 {
      transform: rotateX(225deg) rotateY(0deg) rotateZ(45deg);
    }
    .page {
      position: absolute;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      flex-wrap: wrap;
      overflow: hidden;
      vertical-align: middle;
      user-select: none;
      box-sizing: border-box;
      > span {
        display: inline-block;
      }
      &.dice-default {
        background: #eee;
        border: 1px solid #000;
        > span {
          background: #000;
          border-radius: 50%;
          box-shadow: 1px 1px 2px inset #666;
        }
        &.page1 {
          > span {
            background: red;
          }
        }
      }
      &.page2 {
        justify-content: space-around;
        transform-origin: right;
        transform: rotateY(-90deg);
      }
      &.page3 {
        transform-origin: left;
        transform: rotateY(90deg);
        > span:nth-child(1) {
          position: absolute;
        }
        > span:nth-child(3) {
          position: absolute;
        }
      }
      &.page4 {
        transform-origin: top;
        transform: rotateX(-90deg);
      }
      &.page5 {
        transform-origin: bottom;
        transform: rotateX(90deg);
        > span:last-child {
          position: absolute;
        }
      }
    }

    &.xs {
      width: 30px;
      height: 30px;
      margin: 10px;
      transform-origin: 50% 50% -15px;
      .page {
        width: 30px;
        height: 30px;
        border-radius: 4px;
        > span {
          width: 7px;
          height: 7px;
        }
        &.page3 {
          > span:nth-child(1) {
            top: 5px;
            left: 5px;
          }
          > span:nth-child(3) {
            bottom: 5px;
            right: 5px;
          }
        }
        &.page4 > span {
          margin: 3px;
        }
        &.page5 > span {
          margin: 3px;
        }
        &.page6 {
          padding: 4px 0;
          transform: translateZ(-30px);
          > span {
            margin: 0 2px;
          }
        }
      }
    }

    &.s {
      width: 50px;
      height: 50px;
      margin: 20px;
      transform-origin: 50% 50% -25px;
      .page {
        width: 50px;
        height: 50px;
        border-radius: 5px;
        > span {
          width: 10px;
          height: 10px;
        }
        &.page3 {
          > span:nth-child(1) {
            top: 8px;
            left: 8px;
          }
          > span:nth-child(3) {
            bottom: 8px;
            right: 8px;
          }
        }
        &.page4 > span {
          margin: 7px;
        }
        &.page5 > span {
          margin: 7px;
        }
        &.page6 {
          padding: 3px 0;
          transform: translateZ(-50px);
          > span {
            margin: 1px 5px;
          }
        }
      }
    }

    &.m {
      width: 80px;
      height: 80px;
      margin: 25px;
      transform-origin: 50% 50% -40px;
      .page {
        width: 80px;
        height: 80px;
        border-radius: 8px;
        > span {
          width: 14px;
          height: 14px;
        }
        &.page3 {
          > span:nth-child(1) {
            top: 12px;
            left: 12px;
          }
          > span:nth-child(3) {
            bottom: 12px;
            right: 12px;
          }
        }
        &.page4 > span {
          margin: 10px;
        }
        &.page5 > span {
          margin: 10px;
        }
        &.page6 {
          padding: 6px 0;
          transform: translateZ(-80px);
          > span {
            margin: 1px 8px;
          }
        }
      }
    }

    &.l {
      width: 120px;
      height: 120px;
      margin: 35px;
      transform-origin: 50% 50% -60px;
      .page {
        width: 120px;
        height: 120px;
        border-radius: 12px;
        > span {
          width: 20px;
          height: 20px;
        }
        &.page3 {
          > span:nth-child(1) {
            top: 20px;
            left: 20px;
          }
          > span:nth-child(3) {
            bottom: 20px;
            right: 20px;
          }
        }
        &.page4 > span {
          margin: 18px;
        }
        &.page5 > span {
          margin: 18px;
        }
        &.page6 {
          padding: 10px 0;
          transform: translateZ(-120px);
          > span {
            margin: 1px 14px;
          }
        }
      }
    }

    &.xl {
      width: 160px;
      height: 160px;
      margin: 40px;
      transform-origin: 50% 50% -80px;
      .page {
        width: 160px;
        height: 160px;
        border-radius: 16px;
        > span {
          width: 27px;
          height: 27px;
        }
        &.page3 {
          > span:nth-child(1) {
            top: 30px;
            left: 30px;
          }
          > span:nth-child(3) {
            bottom: 30px;
            right: 30px;
          }
        }
        &.page4 > span {
          margin: 26px;
        }
        &.page5 > span {
          margin: 26px;
        }
        &.page6 {
          padding: 13px 0;
          transform: translateZ(-160px);
          > span {
            margin: 1px 16px;
          }
        }
      }
    }
  }
}
</style>
