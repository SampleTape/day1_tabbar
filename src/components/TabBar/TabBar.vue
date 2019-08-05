<template>
  <div class="tab-bar">
    <div class="tab-dot" :style="{left: activeLeft}"></div>
    <div
      class="tab-container"
      v-for="item in items"
      v-bind:key="item.index"
      :id="`tab-container-${item.index}`"
      @click="handleClick(item)"
    >
      <div class="tab-icon" :class="isActive(item) ? 'active' : ''">
        <div class="tab-img-active">
          <img :src="item.activeImgSrc" alt="item.title" />
        </div>
        <div class="tab-img-default">
          <img :src="item.imgSrc" alt="item.title" />
        </div>
      </div>
      <div class="tab-text">
        <div class="tab-title" :class="!isActive(item) ? 'show' : 'hide'">{{item.title}}</div>
      </div>
    </div>
  </div>
</template>
<script>
import home from './img/cd-default.svg'
import activeHome from './img/cd-active.svg'
import camera from './img/camera-default.svg'
import activeCamera from './img/camera-active.svg'
import file from './img/file-default.svg'
import activeFile from './img/file-active.svg'
import mine from './img/mine-default.svg'
import activeMine from './img/mine-active.svg'
export default {
  data () {
    return {
      activeItem: 'Home',
      items: [
        {
          index: 0,
          title: 'Home',
          imgSrc: home,
          activeImgSrc: activeHome
        },
        {
          index: 1,
          title: 'Camera',
          imgSrc: camera,
          activeImgSrc: activeCamera
        },
        {
          index: 2,
          title: 'Files',
          imgSrc: file,
          activeImgSrc: activeFile
        },
        {
          index: 3,
          title: 'Profile',
          imgSrc: mine,
          activeImgSrc: activeMine
        }
      ]
    }
  },
  computed: {
    activeLeft() {
      for(let i in this.items) {
        if(this.items[i].title === this.activeItem) {
          return i * 25 + 11.5 + '%'
        }
      }
    }
  },
  methods: {
    handleClick (item) {
      this.activeItem = item.title
    },
    isActive (item) {
      return item.title === this.activeItem
    }
  }
}
</script>
<style lang="scss" scoped>
.tab-bar {
  width: 100%;
  height: 10rem;
  position: fixed;
  bottom: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: space-around;
  background-color: #2c3e50;
  border-radius: 10px;
  .tab-dot {
    position: absolute;
    width: 1rem;
    height: 1rem;
    border-radius: 50%;
    background-color: #3498db;
    bottom: 1.5rem;
    // left: 11.5%;
    transition: all 0.9s;
  }
  .tab-container {
    width: 25%;
    height: 9rem;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    .tab-icon {
      width: 4rem;
      height: 4rem;
      overflow: hidden;
      .tab-img-active {
        width: 100%;
        height: 100%;
        transition: all 1s;
        transform: translate(0,-4rem);
        z-index: 0;
      }
      .tab-img-default {
        width: 100%;
        height: 100%;
        transition: all 1s;
        transform: translate(0, -4rem);
        z-index: 1;
      }
      img {
        width: 100%;
        height: 100%;
      }
      &.active {
        .tab-img-active {
          transform: translate(0,0);
        }
        .tab-img-default {
          // transform: translate(0,4rem);
          opacity: 0;
          transition-delay: 0.5s;
        }
        animation: shake 1s;
      }
    }
    .tab-text {
      width: 5rem;
      color: #8a8a8a;
      font-size: 1.5rem;
      text-align: center;
      .tab-title {
        transition: all 1s;
        &.show {
          opacity: 1;
        }
        &.hide {
          opacity: 0;
        }
      }
    }
  }
}

@keyframes shake{
  0%   {transform: rotate(0deg);}
  25%  {transform: rotate(-30deg);}
  50%  {transform: rotate(-35deg);}
  100% {transform: rotate(0deg);}
}
</style>
