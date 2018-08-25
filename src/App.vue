<template>
  <div id="app">
    <drawer width="200px;" :show.sync="drawerVisibility" :show-mode="showModeValue"
        :placement="showPlacementValue" :drawer-style="{'background-color':'#2ca2f9', width: '200px'}">
        <div slot="drawer">
          <!-- 菜单内容 -->
          <group title="歌单" class="drawer-title">
            <cell title="我喜欢" link="/demo" value="" @click.native="drawerVisibility = false"></cell>
            <cell title="欧美范" link="/demo" value="" @click.native="drawerVisibility = false"></cell>
          </group>
        </div>


      <view-box ref="viewBox" body-padding-top="46px" body-padding-bottom="0">
        <x-header slot="header" class="header"  :left-options="leftOptions" :right-options="rightOptions" :title="title">
              <x-icon slot="overwrite-left" type="navicon" size="35" class="header-left-icon" @click.native="showMore()"></x-icon>
              <x-icon slot="right" type="ios-search" size="35" class="header-right-icon" @click.native="showMore()"></x-icon>
          </x-header>
          <transition name="slide-left">
            <router-view class="child-view"></router-view>
          </transition>
        </view-box>
    </drawer>
  </div>
</template>

<script>
  import {Drawer, Group, Cell, Badge, ViewBox, XHeader} from 'vux';

  export default {
    components: {
        Drawer,
        Group,
        Cell, 
        Badge,
        ViewBox,
        XHeader
    },
    data() {
        return {
            showMenu: true,
            drawerVisibility: false,
            showModeValue: 'push',
            showPlacement: 'left',
            showPlacementValue: 'left'

        };
    },
    methods: {
      back() {

      },
      showMore() {
        this.drawerVisibility = true;
      }
    },
    computed: {
      leftOptions() {
        var vm = this;
        let name = this.$route.name;
        switch (name) {
            case 'Home':
                vm.title = '音乐';
                return { showBack: true, preventGoBack: true, backText: ''};
                break;
            default:
                vm.title = '';
                return { showBack: true, preventGoBack: true };
        }
      },
      rightOptions() {
        var vm = this;
        let name = this.$route.name;
        switch (name) {
            case 'Home':
                return { showMore: false};
                break;
            default:
                return { showMore: false};
        }
      },
    }
  }
</script>

<style>
  @import url('assets/styles/common.css');
  
  #app {
    background: #eee;
    height: 100%;
    width: 100%;
  }

  .header {
    width:100%;
    position: absolute !important;
    left:0;
    top:0;
    z-index:100;
  }
  
  .header-left-icon,
  .header-right-icon {
    fill:#fff;
    position:relative;
    top:-8px;
    left:-3px;
  }

  .header-right-icon {
    left: 3px;
  }

  .drawer-title .weui-cells__title{
    line-height: 3rem;
    color: #fff;
    font-size: 1rem;
  }

  .child-view {
    height: 100%;
    transition: all .5s cubic-bezier(.55,0,.1,1); 
  } 
  .slide-left-enter, .slide-right-leave-active {
      opacity: 0;
      -webkit-transform: translate(50px, 0);
      transform: translate(50px, 0);
  }
  .slide-left-leave-active, .slide-right-enter {
      opacity: 0;
      -webkit-transform: translate(-50px, 0);
      transform: translate(-50px, 0);
  }
</style>
