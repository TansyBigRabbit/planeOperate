<!-- 事件日志 -->
<template>
	<div>
		<p>事件日志<span v-if="!readStatus" class="circle"> <span> 1</span> </span></p>
		<hr />
		<div>
			<el-table
			    :data="eventLogData"
			    stripe
			    height="250"
			    style="width: 100%">
			     <el-table-column
			      prop="eventTime"
			      align="center"
			      label="事件时间" >
			    </el-table-column>
			    <el-table-column
			      prop="eventType" 
			      align="center"
			      label="事件类型" >
			      <template slot-scope="scope">
				    <span class="type0" v-if="scope.row.eventType==0">跑道入侵</span>
				    <span class="type1" v-if="scope.row.eventType==1">手动灯控</span>
				    <span class="type2" v-if="scope.row.eventType==2">自动灯控</span> 
				    </template>
			    </el-table-column>
			    <el-table-column
			      prop="eventObj"
			      align="center"
			      label="对象" >
			    </el-table-column>
			    <el-table-column
			      prop="detail"
			      align="center"
			      label="详情">
			    </el-table-column>
			   <el-table-column label="操作" align="center" min-width="130%"> 
	            <template v-if="scope.row.eventType==0" slot-scope="scope">
	               
	              <el-button v-if="!readStatus" @click="haveRead" type="primary" size="small">标记为已读</el-button>
	            </template>
	          </el-table-column>
			  </el-table>
		</div>
	</div>
</template>

<script>
	export default{
		name:"eventLog",
		props:{
			params03:Object
		},
		watch:{
        params03(obj){
        	if(obj){
        		this.eventLogData.unshift(obj);
        	}
        }
		},
		data(){
			return{
			 readStatus:false,
             eventLogData:[{
             	eventTime:"2019-10-07 21:37:12",
             	eventType:0, //0-跑道入侵 1-手动灯控 2-自动灯控
             	eventObj:"跑道",
             	detail:"航班RQ3256入侵跑道",
             }]
			}
		},
		methods:{
          haveRead(){
            this.readStatus=true;
            this.$emit("haveread",true);
          }
		}
           
	}
</script>

<style>
	.type0{
		color:#F56C6C;
		font-weight: bold;
	}
	.type1{
		color:#E6A23C;
		font-weight: bold;
	}
	.type2{
		color:#000;
		font-weight: bold;
	}
</style>