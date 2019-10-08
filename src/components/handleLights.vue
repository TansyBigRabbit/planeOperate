<!-- 手动灯控 -->
<template>
	<div >
	<div class="flex_box" style="justify-content: space-between;">
		<p>手动灯控</p>
		<p>
		<el-switch
		  v-model="value"
		  active-color="#13ce66"
		  inactive-color="#ddd"
		  @change="switchChange">
		</el-switch>
	</p>
	</div>
   <hr />
	<div style="display: flex;">
		<div style="flex: 1">
			<el-checkbox :disabled="!value" v-model="checked01" @change="checkChange01('checked01','lights01','lights02','checkedAfter01')">灯光联动</el-checkbox>
			<!-- <div class="flex_box" style="flex-wrap: wrap;">
				<span class="light_box" >
					<div class="light_noActive" >L1绿</div>
				</span>
				<span class="line">22</span>
				<span class="light_box">33</span>
			</div> -->
			<div class="flex_box">
				<div class="light_box">
					<div v-for="(item,index) in lights01" @click="clickLight('lights01',index)" class="light_noActive" :id="'lights01'+index" >{{item.name}}</div> 
				</div>
				<div v-if="checkedAfter01" class="line">
					<div style="padding-top: 20px;height:30% "><hr /></div>
					<div style="height: 25%"><hr /></div>
					<div><hr /></div>
				</div>
				<div v-else class="line"></div>
				<div class="light_box">
					<div v-for="(item,index) in lights02" @click="clickLight('lights02',index)" class="light_noActive" :id="'lights02'+index" >{{item.name}}</div> 
				</div>
			</div>
		</div>

		<div style="flex: 1">
			<el-checkbox :disabled="!value" v-model="checked02" @change="checkChange01('checked02','lights03','lights04','checkedAfter02')">灯光联动</el-checkbox>
			<!-- <div class="flex_box" style="flex-wrap: wrap;">
				<span class="light_box" >
					<div class="light_noActive" >L1绿</div>
				</span>
				<span class="line">22</span>
				<span class="light_box">33</span>
			</div> -->
			<div class="flex_box">
				<div class="light_box">
					<div v-for="(item,index) in lights03" @click="clickLight('lights03',index)" class="light_noActive" :id="'lights03'+index" >{{item.name}}</div> 
				</div>
				<div v-if="checkedAfter02" class="line">
					<div style="padding-top: 20px;height:30% "><hr /></div>
					<div style="height: 25%"><hr /></div>
					<div><hr /></div>
				</div>
				<div v-else class="line"></div>
				<div class="light_box">
					<div v-for="(item,index) in lights04" @click="clickLight('lights04',index)" class="light_noActive" :id="'lights04'+index" >{{item.name}}</div> 
				</div>
			</div>
		</div>
	</div>

	</div>
</template>
<script>
	export default{
		name:"handleLights",
		props:{
			params01:Object
		},
		data(){
			return{
             value:true,
             checked01:false,
             checked02:false,
             checkedAfter01:false, 
             checkedAfter02:false, 
             lights01:[{
             	name:"L1绿",
             	check:false
                },{
             	name:"L1红",
             	check:true
                },{
             	name:"L1关",
             	check:false
                }],
             lights02:[{
             	name:"L2绿",
             	check:false
                },{
             	name:"L2红",
             	check:true
                },{
             	name:"L2关",
             	check:false
                }],
            lights03:[{
             	name:"L3绿",
             	check:false
                },{
             	name:"L3红",
             	check:true
                },{
             	name:"L3关",
             	check:false
                }],
            lights04:[{
             	name:"L4绿",
             	check:false
                },{
             	name:"L4红",
             	check:true
                },{
             	name:"L4关",
             	check:false
                }]
			}
		},
		mounted(){
        document.getElementById("lights011").setAttribute("class","light_active_red");
        document.getElementById("lights021").setAttribute("class","light_active_red");
        document.getElementById("lights031").setAttribute("class","light_active_red");
        document.getElementById("lights041").setAttribute("class","light_active_red");
		},
		watch:{ 
		},
		methods:{
		switchChange(){ 
			console.log(this.value);
		},
		checkChange01(check,lights_one,lights_two,checkedAfter){
			console.log(this[check]);
			if(this[check]){
				var lights01 ,lights02;
             for(let i = 0;i<this[lights_one].length;i++){
                if(this[lights_one][i].check){
                	lights01 = i;
                	for(let k = 0;k<this[lights_two].length;k++){
                      if(this[lights_two][k].check){
                      	lights02 = k;
                      	if(lights01==lights02){
                          this[checkedAfter]=true;
                          return
                      	} 
                      }
                  }
                }
             }
             this[check]=false;
             this.$message.info("请先同步灯光状态再进行联动！");
            }else{
             this[checkedAfter]=false;	
            }
		},
		clickLight(name,index){ 
		 if(!this.value){
		 	return;
		 }
		 var that = this;
		 //第一个灯光联动checkbox开启
		 if(this.checked01){
         if(name=="lights01"||name=="lights02"){
         if(this[name][index].check){
             this.closeTogether("lights01","lights02",index)  
         }else{
         	this.changeTogether("lights01","lights02",index)
         }
         }else if(name=="lights03"||name=="lights04"){
         	if(this[name][index].check){
             this.closeTogether("lights03","lights04",index)
         	}else{
         	this.changeTogether("lights03","lights04",index)	
         	}
         }
		 }else{
           //var lightsdata = {};
         if(this[name][index].check){
             this[name][index].check=false;
             document.getElementById(name+index).setAttribute("class","light_noActive"); 
             this.lightsdata = this.createParam(name,"关闭"); 
             that.$emit("listenTochildEvent",this.lightsdata); 
         }else{
			for(let i=0;i<this[name].length;i++){
         		if(this[name][i].check){
			 	this[name][i].check=false;
			 	this.lightsData = this.createParam(name,"关闭"); 
			 	that.$emit("listenTochildEvent",this.lightsdata); 
             	document.getElementById(name+i).setAttribute("class","light_noActive");
         		} 
         	}
         	this[name][index].check=true;
            if(index==0){
             this.lightsdata = this.createParam(name,"开启");
             that.$emit("listenTochildEvent",this.lightsdata); 
             document.getElementById(name+index).setAttribute("class","light_active_green");
            }else if(index==1){
             this.lightsdata = this.createParam(name,"开启"); 
             that.$emit("listenTochildEvent",this.lightsdata); 
             document.getElementById(name+index).setAttribute("class","light_active_red");
            }else{
             this.lightsdata = this.createParam(name,"开启"); 
             that.$emit("listenTochildEvent",this.lightsdata); 
             document.getElementById(name+index).setAttribute("class","light_active_black");
            }
         }
		 } 
		 },
		createParam(name,type){ //0-关闭 1-开启
         var eventTime = this.getCurrentTime();
         var eventObj ="L"+name.substring(name.length-1,name.length);
         var eventType = 1;
         var detail = eventObj+"入口手动"+type;
         return {
         	    eventTime:eventTime,
             	eventType:eventType, //0-跑道入侵 1-手动灯控 2-自动灯控
             	eventObj:eventObj,
             	detail:detail,
         }
		},
		 getCurrentTime(){
         	var date = new Date();
            var year = date.getFullYear();
			var month = this.pad2(date.getMonth()+1); 
			var day = this.pad2(date.getDate()); 
			var hour = this.pad2(date.getHours());
			var minute = this.pad2(date.getMinutes());
			var second = this.pad2(date.getSeconds());
			return year+"-"+month+"-"+day+" "+hour+':'+minute+':'+second 
         },
         pad2(n){ 
         	return n < 10 ? '0' + n : n 
         },
         closeTogether(name1,name2,index){
         	 var that = this;
             this[name1][index].check=false;
             this[name2][index].check=false;
             document.getElementById(name1+index).setAttribute("class","light_noActive"); 
             document.getElementById(name2+index).setAttribute("class","light_noActive"); 
             this.lightsdata = this.createParam(name1,"关闭");
             that.$emit("listenTochildEvent",this.lightsdata);

             setTimeout(function(){
             that.lightsdata = that.createParam(name2,"关闭");
             that.$emit("listenTochildEvent",that.lightsdata);
             },200) 
             
         },
         changeTogether(name1,name2,index){
         	var that = this;
          for(let i=0;i<this[name1].length;i++){
               if(this[name1][i].check){
			 	this[name1][i].check=false;
			 	this.lightsData = this.createParam(name1,"关闭"); 
			 	that.$emit("listenTochildEvent",this.lightsdata); 
             	document.getElementById(name1+i).setAttribute("class","light_noActive");
         		} 
         	} 
         	for(let k=0;k<this[name2].length;k++){
               if(this[name2][k].check){
			 	this[name2][k].check=false;
			 	this.lightsData = this.createParam(name2,"关闭"); 
			 	that.$emit("listenTochildEvent",this.lightsdata); 
             	document.getElementById(name2+k).setAttribute("class","light_noActive");
         		} 
         	}
            this[name1][index].check=true;
            this[name2][index].check=true;
            if(index==0){
             this.lightsdata = this.createParam(name1,"开启");
             that.$emit("listenTochildEvent",this.lightsdata); 
             setTimeout(function(){
             that.lightsdata = that.createParam(name2,"开启");
             that.$emit("listenTochildEvent",that.lightsdata);
             },200);
              document.getElementById(name1+index).setAttribute("class","light_active_green");

             document.getElementById(name2+index).setAttribute("class","light_active_green");
            }else if(index==1){
             this.lightsdata = this.createParam(name1,"开启"); 
             that.$emit("listenTochildEvent",this.lightsdata); 
             setTimeout(function(){
             that.lightsdata = that.createParam(name2,"开启");
             that.$emit("listenTochildEvent",that.lightsdata);
             },200);
             document.getElementById(name1+index).setAttribute("class","light_active_red");
             document.getElementById(name2+index).setAttribute("class","light_active_red");
            }else{
             this.lightsdata = this.createParam(name1,"开启"); 
             that.$emit("listenTochildEvent",this.lightsdata); 
             document.getElementById(name1+index).setAttribute("class","light_active_black");
			 setTimeout(function(){
             that.lightsdata = that.createParam(name2,"开启");
             that.$emit("listenTochildEvent",that.lightsdata);
             },200);
             document.getElementById(name2+index).setAttribute("class","light_active_black");
            }
         },
		}
	}
</script>

<style>
	.light_box{
		width: 35%;
		text-align: center;

	}
	.light_box>div{ 
		border-radius: 5px;
		box-sizing: border-box;
		width: 70%;
		margin: 10px auto;
		padding: 5px 10px;
		cursor: pointer;
	}
	.light_active_red{
	 border: 2px solid #F56C6C;	
	 color: #F56C6C;
	}
	.light_active_green{
	 border: 2px solid #67C23A;	
	 color: #67C23A;
	}
	.light_active_black{
	 border: 2px solid #000;	
	 color: #000;
	}
	.light_noActive{
	 border: 2px solid #ddd;	
     color:#ddd;
	}
	.line{
		width: 20%;
		text-align: center;
	}
	.line>div{
		height: 33%
	}
	hr{
		color: #ddd
	}
</style>