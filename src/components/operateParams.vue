<!-- 运行参数 -->
<template>
	<div>
		<p>运行参数</p>
		<el-tabs v-model="activeName" type="card" @tab-click="handleClick">
	    <el-tab-pane label="静态参数" name="tab01">
	    	<div><el-table
			    :data="staticParams"
			    stripe
			    style="width: 100%">
			     <el-table-column
			      prop="paramCode"
			      align="center"
			      label="参数编号" >
			    </el-table-column>
			    <el-table-column
			      prop="paramName"
			      align="center"
			      label="参数名称" >
			    </el-table-column>
			    <el-table-column
			      prop="value"
			      align="center"
			      label="参数值" >
			    </el-table-column>
			    <el-table-column
			      prop="unit"
			      align="center"
			      label="参数单位">
			    </el-table-column> 
			  </el-table>
			</div>
	    </el-tab-pane>
	    <el-tab-pane label="五边参数" name="tab02">
	    <div>
	    	<el-table
			    :data="fiveParams"
			    stripe
			    style="width: 100%">
			     <el-table-column
			      prop="paramCode"
			      align="center"
			      label="参数编号" >
			    </el-table-column>
			    <el-table-column
			      prop="paramName"
			      align="center"
			      label="参数名称" >
			    </el-table-column>
			    <el-table-column
			      prop="value"
			      align="center"
			      label="参数值" >
			    </el-table-column>
			    <el-table-column
			      prop="unit"
			      align="center"
			      label="参数单位">
			    </el-table-column> 
			  </el-table>
			</div>
		</el-tab-pane>
	    <el-tab-pane label="跑道参数" name="tab03">
	    <div>
	    	<el-table
			    :data="traceParams"
			    stripe
			    style="width: 100%">
			     <el-table-column
			      prop="paramCode"
			      align="center"
			      label="参数编号" >
			    </el-table-column>
			    <el-table-column
			      prop="paramName"
			      align="center"
			      label="参数名称" >
			    </el-table-column>
			    <el-table-column
			      prop="value"
			      align="center"
			      label="参数值" >
			    </el-table-column>
			    <el-table-column
			      prop="unit"
			      align="center"
			      label="参数单位">
			    </el-table-column> 
			  </el-table>
			</div>
		</el-tab-pane>
	    <el-tab-pane label="起降参数" name="tab04">
		 <div>
	    	<el-table
			    :data="takeOnParams"
			    stripe
			    style="width: 100%">
			     <el-table-column
			      prop="paramCode"
			      align="center"
			      label="参数编号" >
			    </el-table-column>
			    <el-table-column
			      prop="paramName"
			      align="center"
			      label="参数名称" >
			    </el-table-column>
			    <el-table-column
			      prop="value"
			      align="center"
			      label="参数值" >
			    </el-table-column>
			    <el-table-column
			      prop="unit"
			      align="center"
			      label="参数单位">
			    </el-table-column> 
			  </el-table>
			</div>
	    </el-tab-pane>
	    <el-tab-pane label="规则参数" name="tab05">
	    	<div>
	    	<el-table
			    :data="ruleParams"
			    stripe
			    style="width: 100%">
			     <el-table-column
			      prop="paramCode"
			      align="center"
			      label="参数编号" >
			    </el-table-column>
			    <el-table-column
			      prop="paramName"
			      align="center"
			      label="参数名称" >
			    </el-table-column>
			    <el-table-column
			      prop="value"
			      align="center"
			      label="参数值" >
			    </el-table-column>
			    <el-table-column
			      prop="unit"
			      align="center"
			      label="参数单位">
			    </el-table-column> 
			  </el-table>
			</div>
	    </el-tab-pane>
	  </el-tabs>
	</div>
</template>

<script>
	export default{
		name:"operateParams",
		props:{
			params05:Object
		},
		data(){
			return{
              activeName:"tab01",
              staticParams:[{
              	paramCode:'P1.1',
              	paramName:'跑道端点1位置',
              	value:353.335,
              	unit:'WGS84坐标'
              },{
              	paramCode:'P1.2',
              	paramName:'跑道端点2位置',
              	value:225.224,
              	unit:'WGS84坐标'
              },{
              	paramCode:'P1.3',
              	paramName:'跑道海拔高度',
              	value:27,
              	unit:'米'
              },{
              	paramCode:'P1.4',
              	paramName:'跑道宽度',
              	value:60,
              	unit:'米'
              }],
              //
               fiveParams:[{
              	paramCode:'P2.1',
              	paramName:'五边区域计算点',
              	value:900,
              	unit:'米'
              },{
              	paramCode:'P2.2',
              	paramName:'五边区域计算角度',
              	value:15,
              	unit:'米'
              },{
              	paramCode:'P2.3',
              	paramName:'五边区域延伸距离',
              	value:20000,
              	unit:'米'
              },{
              	paramCode:'P2.4',
              	paramName:'五边区域延伸高度',
              	value:1000,
              	unit:'米'
              }],
              //
              traceParams:[{
              	paramCode:'P3.1',
              	paramName:'跑道飞行区范围',
              	value:75,
              	unit:'米'
              },{
              	paramCode:'P3.2',
              	paramName:'跑道盲降信号敏感区范围',
              	value:90,
              	unit:'WGS84坐标'
              },{
              	paramCode:'P3.3',
              	paramName:'交流道封闭区域',
              	value:256.665,
              	unit:'米'
              }],
              //
              takeOnParams:[{
              	paramCode:'P4.1',
              	paramName:'降落滑行开始判定高度',
              	value:0,
              	unit:'米'
              },{
              	paramCode:'P4.2',
              	paramName:'降落判定高度',
              	value:100,
              	unit:'米'
              },{
              	paramCode:'P4.3',
              	paramName:'起飞过程判定速度',
              	value:55,
              	unit:'米'
              },{
              	paramCode:'P4.4',
              	paramName:'起飞判定高度',
              	value:100,
              	unit:'米'
              }],
              //
              ruleParams:[{
              	paramCode:'P5.1',
              	paramName:'降落目标下降梯度',
              	value:6.5,
              	unit:'米'
              },{
              	paramCode:'P5.2',
              	paramName:'降落优现保留距离',
              	value:14000,
              	unit:'米'
              },{
              	paramCode:'P5.3',
              	paramName:'跑道上空占用高度',
              	value:100,
              	unit:'米'
              }],
			}
		},
		methods:{
		handleClick(e){
			console.log(e);
		}
		},

	}
</script>