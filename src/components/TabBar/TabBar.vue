<template>
  <div class="tab-bar">
    <div class="tab-dot"></div>
    <div class="tab-container" v-for="item in items" v-bind:key="item.index" :id="`tab-container-${item.index}`" @click="handleClick(item)">
      <div class="tab-icon">
        <div v-if="isActive(item)" class="tab-img active">
          <img :src="item.activeImgSrc" alt="item.title">
        </div>
        <div v-if="!isActive(item)" class="tab-img default">
          <img :src="item.imgSrc" alt="item.title">
        </div>
      </div>
      <div class="tab-text">
          <div class="tab-title" v-if="!isActive(item)">{{item.title}}</div>
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
      activeColor: '#8e44ad',
      defaultColor: '#2c3e50',
      activeItem: 'Home',
      items: [
        {
          title: 'Home',
          imgSrc: home,
          activeImgSrc: activeHome
        },
        {
          title: 'Camera',
          imgSrc: camera,
          activeImgSrc: activeCamera
        },
        {
          title: 'Files',
          imgSrc: file,
          activeImgSrc: activeFile
        },
        {
          title: 'Profile',
          imgSrc: mine,
          activeImgSrc: activeMine
        }
      ]
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
    left: 7.5rem;
    transition: all 1s;
  }
  .tab-container {
    width: 9rem;
    height: 9rem;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    .tab-text {
      width: 5rem;
      color: #8a8a8a;
      font-size: 1.5rem;
      text-align: center;
    }
    img {
      width: 4rem;
      height: 4rem;
    }
  }
    
}
</style>
