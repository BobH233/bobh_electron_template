<template>
  <div id="app">
    <div id="titleBar">
      <div id="closeBtn" @click="closeWindow"></div>
      <div id="minSizeBtn" @click="minWindow"></div>
      <div id="maxSizeBtn" @click="maxWindow"></div>
      <div id="titleText">{{title}}</div>
    </div>
    <router-view id="rt"/>
  </div>
</template>
<script>

//const axios = require("axios");
const { remote } = require('electron')

export default {
  name:"Home",
  data(){
    return {
      title:"untitled",
    }
  },
  created(){
    this.setTitle("BobH的Electron+vue模板");
  },
  methods:{
    getTitle: ()=>{
      return remote.BrowserWindow.getAllWindows()[0].getTitle();
    },
    setTitle: function(ttt){
      let that = this;
      this.title = ttt;
      remote.BrowserWindow.getAllWindows()[0].setTitle(ttt);
    },
    closeWindow(){
      remote.BrowserWindow.getFocusedWindow().close();
    },
    minWindow(){
      remote.BrowserWindow.getFocusedWindow().minimize();
    },
    maxWindow(){
      if(remote.BrowserWindow.getFocusedWindow().isMaximized())
        remote.BrowserWindow.getFocusedWindow().restore();
      else
        remote.BrowserWindow.getFocusedWindow().maximize();
    }
  },
}
</script>

<style src="./assets/main.css">