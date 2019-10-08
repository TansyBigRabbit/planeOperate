<!-- 起降日志 -->
<template>
	<div >
		<div><p>起降日志</p></div>
    <hr />
		<div>
			 <el-table
       stripe
    ref="filterTable"
    :data="tableData"
    height="290" >
    <el-table-column
      type="index"
      label="序号"
      align="center"
      sortable   
    >
    </el-table-column>
    <el-table-column
      prop="flightNum"
      label="航班号"
      align="center" >
    </el-table-column>
    
    <el-table-column
      prop="event"
      label="事件"
      align="center" 
      :filters="[{ text: '起飞', value: '起飞' }, { text: '降落', value: '降落' }]"
      :filter-method="filterTag"
      filter-placement="bottom-end">
      <template slot-scope="scope">
        <el-tag
          :type="scope.row.event === '起飞' ? 'primary' : 'success'"
          disable-transitions>{{scope.row.event}}</el-tag> 
          
      </template>
    </el-table-column>
    <el-table-column
      prop="takeOffTime"
      align="center"
      label="时间" >
    </el-table-column>
  </el-table>
		</div>
	</div>
</template>

<script>
	export default{
		name:"takeOffLog",
		props:{
			params04:Object
		},
		data(){
			return{
          	tableData: [{
	          	flightNum: 'FH7788',
	          	event: '起飞',
	          	takeOffTime: '23:56:08', 
		        }, {
		          flightNum: 'FH7788',
		          event: '降落',
		          takeOffTime: '23:56:08', 
		        },{
		          flightNum: 'FH7788',
		          event: '降落',
		          takeOffTime: '23:56:08', 
		        },{
		          flightNum: 'FH7788',
		          event: '起飞',
		          takeOffTime: '23:56:08', 
		        },{
		          flightNum: 'FH7788',
		          event: '起飞',
		          takeOffTime: '23:56:08', 
		        },]
			}
		},
		methods:{  
      filterTag(value, row) {
        return row.event === value;
      },
      filterHandler(value, row, column) {
        const property = column['property'];
        return row[property] === value;
      }
		}
	}
</script>