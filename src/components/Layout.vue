<template>
<div class="foxgis-layout">
  <div class="mdl-layout mdl-js-layout">
    <header class="mdl-layout__header mdl-layout__header--seamed">
      <div class="mdl-layout__header-row">
        <div class="mdl-layout-spacer"></div>
        <h5>管理员</h5>
        <nav class="mdl-navigation">
          <a class="mdl-navigation__link" v-link="{ path: '/loginManagement' }" v-if="username==undefined">登录</a>
          <a class="mdl-navigation__link" v-else>{{username}}</a>
        </nav>
      </div>
    </header>
    <div class="mdl-layout--content">
      <slot>Layout content</slot>
    </div>
  </div>
</div>
</template>


<script>
import Cookies from 'js-cookie'
export default {
  methods: {
    signout: function(){
      Cookies.remove('super-username');
      Cookies.remove('super-access_token');
      Cookies.remove('super-name');
      Cookies.remove('super-phone');
      Cookies.remove('super-email');
      Cookies.remove('super-location');
      Cookies.remove('super-organization');
      window.location.href = '/loginManagement';
    },

    showUserCenter: function(){
      if(document.querySelector('.userCenter').style.display === 'none'){
        document.querySelector('.userCenter').style.display = 'block';
      }else{
        document.querySelector('.userCenter').style.display = 'none';
      }  
    }
  },
  ready() {
    /*global componentHandler */
    componentHandler.upgradeElement(this.$el.firstElementChild);
  },
  attached: function() {
    //判断是否登陆
    let username = Cookies.get('super-username');
    if(username !== undefined){
      this.username = username;
    }
  },
  data: function(){
    return {
      username: undefined
    }
  }
}

</script>


<style scoped>
.mdl-layout__header {
  height: 100px;
  background-image: url('../assets/header.jpg');
  background-size: contain;
  background-repeat: no-repeat;
  background-color: #3861CB;
}

.mdl-layout.has-drawer .mdl-layout__header > .mdl-layout-icon {
  display: block;
  width: 48px;
  height: 48px;
  top: 8px;
}

.mdl-layout__header-row {
  height: 100px;
}

.mdl-layout-title {
  font-size: 1.5em;
}

.mdl-navigation{
  line-height: 30px;
  position: relative;
  top: 34px;
  left: 40px;
}

.mdl-navigation .v-link-active{
  background-color: rgb(15, 199, 251);
}

.mdl-layout__header-row .mdl-navigation__link {
  font-size: 1em;
  line-height: 30px;
  padding: 0 10px;
  cursor: pointer;
}

.mdl-layout--content {
  height: 100%;
  position:relative;
  min-height: calc(100% - 100px);
  background-color: #e4e4e4;
  display: flex;
  flex-flow: column;
}

a.disabled {
   pointer-events: none;
   cursor: default;
}

.download_link{
  cursor: pointer;
}

.userCenter{
  height: 60px;
  width: 110px;
  z-index: 9999;
  position: absolute;
  right: 0;
  background-color: #3f51b5;
  text-align: center;
  line-height: 30px;
  display: none;
}

.userCenter a{
  display: inherit;
  cursor: pointer;
  color: #fff;
  text-decoration: none;
}

</style>
