<template>
	<div class="bg_content">
<!-- <div class="line"></div> -->
<el-menu
  :default-active="activeIndex"
  class="el-menu-demo"
  mode="horizontal"
  @select="handleSelect"
  background-color="#545c64"
  text-color="#fff"
  active-text-color="#ffd04b">
  <el-menu-item index="1">综合监控</el-menu-item>
  <el-menu-item index="2">跑道防入侵
  	<span v-if="!readStatus" class="circle"> <span> 1</span> </span> </el-menu-item>   
</el-menu>
<div class="main_content">
<div class="part1" style="display: flex">
<!--起飞降落队列-->
<takeOffQueue style="flex: 5;margin-bottom: 10px" :params02="params02" @getLightsData01="getLightsData($event)"></takeOffQueue> 
<!--起降日志-->
<takeOffLog class="item_box" style="flex: 1;" :params04="params04"></takeOffLog>
<!--事件日志-->
<eventLog  class="item_box" style="flex: 2;margin-right: 0px" :params03="params03" v-on:haveread="haveReadAlert" ></eventLog> 
</div>
<div class="part2" style="display: flex">
  <!--场面动态-->
<sceneStatus class="item_box" style="flex: 3"  :params06="params06"></sceneStatus> 
<div style="flex: 1">
 <!--手动控灯-->
<handleLights style="margin-right: 0px" class="item_box"  :params01="params01" v-on:listenTochildEvent="showMessageFromChild"></handleLights> 
<!--运行参数-->
<operateParams style="margin-right: 0px" class="item_box"  :params04="params05"></operateParams>
</div>
</div>
</div>
</div>
</template>

<script>
	import handleLights from './handleLights'
	import takeOffQueue from './takeOffQueue'
	import takeOffLog from './takeOffLog'
	import operateParams from './operateParams'
	import eventLog from './eventLog'
	import sceneStatus from './sceneStatus'
	export default{
     components:{
     	handleLights,takeOffQueue,eventLog,takeOffLog,operateParams,sceneStatus
     },
     data(){
     	return{
        readStatus:false,
     	//传给手动灯控组件的参数
		params01:{
			name:111
		},
		//传给降落/起飞队列组件的参数
		params02:{
			name:111
		},
		//传给事件日志的参数
		params03:null,
		//传给起降日志的参数
		params04:{},
		//传给运行参数的参数
		params05:{},
		//
		params06:{},
		activeIndex: '1', 
     	}
     },
     methods:{
     	showMessageFromChild(e){ 
         console.log(e);
         this.params03=e;
     	},
     	handleSelect(key, keyPath) {
        console.log(key, keyPath);
      },
      haveReadAlert(e){
      	this.readStatus = e;
      }
     }
	}
</script>

<style>
	.flex_box{
		display: flex;
		flex-wrap: wrap;
	}
    .flex_column{
    	display: flex;
    	flex-direction: column;
    	flex-wrap: wrap;
    }
    .circle{
     border-radius: 50%;
     height: 20px;
     width: 20px;
     display: inline-block;
     background: #f30303;
     margin-left: 5px
    }
    .circle>span{
    display: block;
    color: #FFFFFF;
    height: 20px;
    line-height: 20px;
    text-align: center
    }
    .el-table__row tr{
    max-height: 50px;
 }
 .bg_content{
  background-color: #F0FFFF
 }
 .main_content{
  padding: 15px
 }
 .item_box{
  background-color: #fff;
  padding: 0 10px;
  border: 1px solid #ddd;
  box-sizing: border-box;
  box-shadow: 1px 1px 6px #ddd;
  margin-right: 10px;
  margin-bottom: 10px;
 }
 hr{
  color: #ddd
 }
</style>