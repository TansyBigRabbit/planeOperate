<template>
	<div>
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
<!-- <operateParams style="width: 600px;padding: 15px;height: 300px" :params04="params05"></operateParams> -->
<!-- <takeOffLog style="width: 600px;padding: 15px;height: 300px" :params04="params04"></takeOffLog> -->
<!-- <handleLights style="width: 300px;padding: 15px;height: 300px" :params01="params01" v-on:listenTochildEvent="showMessageFromChild"></handleLights> -->
<!-- <takeOffQueue style="width: 600px;padding: 15px;height: 300px" :params02="params02" @getLightsData01="getLightsData($event)"></takeOffQueue> -->
 <eventLog style="width: 600px;padding: 15px;height: 300px" :params03="params03" v-on:haveread="haveReadAlert" ></eventLog>   
<!-- <sceneStatus style="width: 600px;padding: 15px;height: 300px" :params06="params06"></sceneStatus> -->
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
</style>