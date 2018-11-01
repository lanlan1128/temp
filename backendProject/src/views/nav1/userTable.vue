<template>
	<section>
		<!--列表-->
		<el-table :data="users" highlight-current-row v-loading="listLoading" @selection-change="selsChange" style="width: 100%;">
			<el-table-column prop="index" label="序号" width="80">
			</el-table-column>
			<el-table-column prop="name" label="用户ID" width="120" sortable>
			</el-table-column>
			<el-table-column prop="sex" label="昵称" width="100" :formatter="formatSex" sortable>
			</el-table-column>
			<el-table-column prop="age" label="头像" width="100" sortable>
			</el-table-column>
			<el-table-column prop="birth" label="注册时间" width="120" sortable>
			</el-table-column>
			<el-table-column prop="age" label="当前金币数" min-width="180" sortable align="right">
			</el-table-column>
			<el-table-column prop="age" label="连续签到天数" min-width="180" sortable align="right">
			</el-table-column>
			<el-table-column prop="age" label="本月获取金币数" min-width="180" sortable align="right">
			</el-table-column>
			<el-table-column prop="age" label="近90天获取的金币数" min-width="180" sortable align="right">
			</el-table-column>
		</el-table>

		<!--工具条-->
		<el-col :span="24" class="toolbar">
			<el-pagination layout="prev, pager, next" @current-change="handleCurrentChange" :page-size="20" :total="total" style="float:right;">
			</el-pagination>
		</el-col>
	</section>
</template>

<script>
	import { getUserListPage} from '../../api/api';

	export default {
		data() {
			return {
				users: [],
				total: 0,
				page: 1,
				listLoading: false,
			}
		},
		methods: {
			//性别显示转换
			formatSex: function (row, column) {
				return row.sex == 1 ? '男' : row.sex == 0 ? '女' : '未知';
			},
			// 切换页数
			handleCurrentChange(val) {
				this.page = val;
				this.getUsers();
			},
			//获取用户列表
			getUsers() {
				let para = {
					page: this.page,
				};
				this.listLoading = true;

				getUserListPage(para).then((res) => {
					this.total = res.data.total;
					this.users = res.data.users;
					this.listLoading = false;
				});
			},
		},
		mounted() {
			this.getUsers();
		}
	}

</script>

<style scoped>

</style>