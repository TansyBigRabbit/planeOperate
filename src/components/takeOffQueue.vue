<!-- 当前降落/起飞队列 -->
<template>
	<div class="flex_box">
		<div style="flex:1">
			<div class="flex_box" style="justify-content: space-between;
			">
				<span>当前降落队列</span>
				<span>{{currentTime}}</span>
			</div><hr/>
			<transition name="el-zoom-in-top">
			<div v-show="showTable01">
				<el-table
			    :data="descentList"
			    stripe
			    style="width: 100%">
			     <el-table-column
			      prop="index"
			      align="center"
			      label="序号" >
			    </el-table-column>
			    <el-table-column
			      prop="flightNum"
			      align="center"
			      label="航班号" >
			    </el-table-column>
			    <el-table-column
			      prop="etat"
			      align="center"
			      label="ETAT" >
			    </el-table-column>
			    <el-table-column
			      prop="distance"
			      align="center"
			      label="距跑道">
			    </el-table-column>
			    <el-table-column
			      prop="beforeDis"
			      align="center"
			      label="前/后间距">
			    </el-table-column>
			  </el-table>
			 </div>
			 </transition>
		</div>

		<div style="flex:1">
			<div class="flex_box" style="justify-content: space-between;
			">
				<span>当前起飞队列</span>
				<span>{{currentTime}}</span>
			</div><hr/>
			<transition name="el-zoom-in-top">
			<div v-show="showTable01">
				<el-table
			    :data="takeOffList"
			    stripe
			    style="width: 100%">
			     <el-table-column
			      prop="index"
			      align="center"
			      label="序号" >
			    </el-table-column>
			    <el-table-column
			      prop="flightNum"
			      align="center"
			      label="航班号" >
			    </el-table-column>
			    <el-table-column
			      prop="traceEnter"
			      align="center"
			      label="跑道入口" >
			    </el-table-column>
			    <el-table-column
			      prop="takeOffTime"
			      align="center"
			      label="预计起飞时间">
			    </el-table-column> 
			  </el-table>
			 </div>
			 </transition>
		</div>
	</div>
</template>

<script>
	export default{
		name:"takeOffQueue",
		props:{
			params02:Object
		},
		data(){
			return{
             currentTime:"",
             //当前页码
             currentPage01:1,
             currentPage02:1,
             showTable01:true,
             //降落数据
             descentList:[{
            	index:1,
             	flightNum:"BX5504",
             	etat:"19:05:00",
             	distance:'-1.5',
             	beforeDis:"0/4.5"
             },{
             	index:2,
             	flightNum:"XG5468",
             	etat:"19:25:00",
             	distance:'3',
             	beforeDis:"3/10"
             },{
             	index:3,
             	flightNum:"XD1225",
             	etat:"20:35:10",
             	distance:'13',
             	beforeDis:"10/7"
             },{
             	index:4,
             	flightNum:"HJ8988",
             	etat:"20:57:32",
             	distance:'20',
             	beforeDis:"7/25"
             },{
             	index:5,
             	flightNum:"YV9999",
             	etat:"21:07:07",
             	distance:'45',
             	beforeDis:"25/-"
             },],
             //起飞数据
            takeOffList:[{
            	index:1,
             	flightNum:"BX5504",
             	takeOffTime:"19:15:30",
             	traceEnter:'L2' 
             },{
             	index:2,
             	flightNum:"XG5468",
             	takeOffTime:"21:32:23",
             	traceEnter:'L1' 
             },{
             	index:3,
             	flightNum:"XD1225",
             	takeOffTime:"20:17:12",
             	traceEnter:'L1' 
             },{
             	index:4,
             	flightNum:"HJ8988",
             	takeOffTime:"22:05:09",
             	traceEnter:'L2' 
             },{
             	index:5,
             	flightNum:"YV9999",
             	takeOffTime:"23:55:00",
             	traceEnter:'L3' 
             },],
			}
		},
		created(){
			setInterval(this.getCurrentTime,1000);
            setInterval(this.autoPage,5000);
		},
		methods:{
         getCurrentTime(){
         	var date = new Date();
            var year = date.getFullYear();
			var month = this.pad2(date.getMonth()+1); 
			var day = this.pad2(date.getDate()); 
			var hour = this.pad2(date.getHours());
			var minute = this.pad2(date.getMinutes());
			var second = this.pad2(date.getSeconds());
			this.currentTime = year+"-"+month+"-"+day+" "+hour+':'+minute+':'+second 
         },
         pad2(n){ 
         	return n < 10 ? '0' + n : n 
         },
         //两个表格自动翻页
         autoPage(){ 
          var that = this;
          this.showTable01 = false;
          if(that.currentPage01==1){
          	that.currentPage01+=1;
          	this.descentList = [{
          		index:6,
             	flightNum:"CJ8899",
             	etat:"21:25:00",
             	distance:'13',
             	beforeDis:"2/5.5"
             },{
             	index:7,
             	flightNum:"DH7728",
             	etat:"21:37:50",
             	distance:'5',
             	beforeDis:"3/10"
             },{
             	index:8,
             	flightNum:"BU3368",
             	etat:"22:07:17",
             	distance:'8',
             	beforeDis:"0/6"
             },{
             	index:9,
             	flightNum:"JK9999",
             	etat:"22:17:22",
             	distance:'35',
             	beforeDis:"8/0"
             },{
             	index:10,
             	flightNum:"YV7777",
             	etat:"23:07:07",
             	distance:'25',
             	beforeDis:"7/8"
             },];
             this.takeOffList=[{
            	index:6,
             	flightNum:"BX5504",
             	takeOffTime:"19:15:30",
             	traceEnter:'L2' 
             },{
             	index:7,
             	flightNum:"XG5468",
             	takeOffTime:"21:32:23",
             	traceEnter:'L1' 
             },{
             	index:8,
             	flightNum:"XD1225",
             	takeOffTime:"20:17:12",
             	traceEnter:'L1' 
             },{
             	index:9,
             	flightNum:"HJ8988",
             	takeOffTime:"22:05:09",
             	traceEnter:'L2' 
             },{
             	index:10,
             	flightNum:"YV9999",
             	takeOffTime:"23:55:00",
             	traceEnter:'L3' 
             },]
          }else{
            that.currentPage01=1;
            this.descentList = [{
            	index:1,
             	flightNum:"BX5504",
             	etat:"19:05:00",
             	distance:'-1.5',
             	beforeDis:"0/4.5"
             },{
             	index:2,
             	flightNum:"XG5468",
             	etat:"19:25:00",
             	distance:'3',
             	beforeDis:"3/10"
             },{
             	index:3,
             	flightNum:"XD1225",
             	etat:"20:35:10",
             	distance:'13',
             	beforeDis:"10/7"
             },{
             	index:4,
             	flightNum:"HJ8988",
             	etat:"20:57:32",
             	distance:'20',
             	beforeDis:"7/25"
             },{
             	index:5,
             	flightNum:"YV9999",
             	etat:"21:07:07",
             	distance:'45',
             	beforeDis:"25/-"
             },];

             this.takeOffList=[{
            	index:1,
             	flightNum:"BX5504",
             	takeOffTime:"19:15:30",
             	traceEnter:'L2' 
             },{
             	index:2,
             	flightNum:"XG5468",
             	takeOffTime:"21:32:23",
             	traceEnter:'L1' 
             },{
             	index:3,
             	flightNum:"XD1225",
             	takeOffTime:"20:17:12",
             	traceEnter:'L1' 
             },{
             	index:4,
             	flightNum:"HJ8988",
             	takeOffTime:"22:05:09",
             	traceEnter:'L2' 
             },{
             	index:5,
             	flightNum:"YV9999",
             	takeOffTime:"23:55:00",
             	traceEnter:'L3' 
             },]
          }
           setTimeout(function(){
          	that.showTable01 = true;
          },500)
         },
		}
	}
</script>
<style>
	
</style>