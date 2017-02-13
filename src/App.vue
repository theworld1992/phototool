<template>
  <div id="app">
    <div id="nav">
      <h2 class="logobox"><p><i class="fa fa-skyatlas" aria-hidden="true"></i></p><span>XX</span></h2>
      <ul class="userlist">
        <li class="compile"><a href=""><i class="fa fa-gear" aria-hidden="true"></i><span>编辑图片</span></a></li>
        <li class="myphoto"><a href=""><i class="fa fa-list" aria-hidden="true"></i><span>我的图片</span></a></li>
        <li class="photogallery"><a href=""><i class="fa fa-500px" aria-hidden="true"></i><span>图库</span></a></li>
        <li class="callme"><a href=""><i class="fa fa-phone" aria-hidden="true"></i><span>联系我</span></a></li>
      </ul>
    </div>
    <div id="content"> 
      <core></core>  
    </div>
    <div id="range"></div>
    <div id="photostyle"></div>
  </div>
</template>

<script>
import core from 'components/core.vue'
export default {
  components:{
    core,
  }
}
</script>

<style src="../static/font-awesome-4.7.0/css/font-awesome.min.css"></style> 
<style>

html, body {
  height: 100%;
  font-family: 'Source Sans Pro', 'Helvetica Neue', Arial, sans-serif;
  color: #34495e;
}
* {
  margin: 0;
  padding: 0;
}
a {
  text-decoration: none;
  color: #34495e;
}
ul {
  list-style: none;
}
#app {
  width: 100%;
  height: 100%;
  background-color: rgb(234,234,234);
  display: flex;
}
#nav {
  width: 230px;
  min-width: 180px;
  height: 100%;
  background-color: rgb(234, 234, 234);
  display: flex;
  flex-direction: column;
  border-right: 4px solid rgb(209, 209, 209);
}
#content {
  flex-grow: 1;
  min-width: 600px;
  width: 100%;
  height: 100%;
  border-right: 4px solid rgb(209, 209, 209);
}
#range {
  width: 270px;
  background-color: rgb(234,234,234);
}
.logobox {
  font-size: 26px;
  display: flex;
  line-height: 30px;
  height: 50px;
  background-color: rgb(72, 159, 223);
  vertical-align: middle;
  padding: 10px 0 10px 10px;
  box-sizing: border-box;
  border-radius: 5px;
}
.logobox i {
  font-size: 36px;
  color: rgb(234, 234, 234);
}
.logobox span {
  margin-left: 30px;
  color: #fff;
}
.userlist {
  padding: 10px 0 10px 10px;
  box-sizing: border-box;
  height: 100%;
  display: flex;
  flex-direction: column;
}
.userlist li {
  margin: 10px 0;
}
.userlist li a {
  font-size: 20px;
}
.userlist li span {
  margin-left: 10px;
}
.userlist li:hover span {
  color: #ff6700;
}
</style>
