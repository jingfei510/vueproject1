<template>



	<div id="div1">
		<el-row>
			<el-col :span="8">
				<div class="grid-content bg-purple">

					<el-form ref="form" :model="user" label-width="80px">
						<el-form-item label="学号">
							<el-input v-model="user.id"></el-input>
						</el-form-item>
						<el-form-item label="姓名">
							<el-input v-model="user.name"></el-input>
						</el-form-item>
						<el-form-item label="性别">
							<el-radio-group v-model="user.sex">
								<el-radio label="男"></el-radio>
								<el-radio label="女"></el-radio>
							</el-radio-group>
						</el-form-item>
						<el-form-item label="籍贯">
							<el-select v-model="user.adress" placeholder="请选择籍贯">
								<el-option label="陕西" value="陕西"></el-option>
								<el-option label="湖南" value="湖南"></el-option>
							</el-select>
						</el-form-item>

						<el-form-item label="兴趣爱好">
							<el-checkbox-group v-model="user.hobbies">
								<el-checkbox label="唱歌" name="type"></el-checkbox>
								<el-checkbox label="跑步" name="type"></el-checkbox>
								<el-checkbox label="玩游戏" name="type"></el-checkbox>

							</el-checkbox-group>
						</el-form-item>

						<el-form-item label="备注">
							<el-input type="textarea" v-model="user.beizhu"></el-input>
						</el-form-item>
						<el-form-item>
							<el-button type="primary" @click="adduser">添加</el-button>
							<el-button type="primary" @click="updateuser(user)">修改</el-button>
						</el-form-item>

					</el-form>

				</div>
			</el-col>
			<el-col :span="2">
				<div class="grid-content bg-purple-light">&nbsp;</div>
			</el-col>
			<el-col :span="14">
				<div class="grid-content bg-purple-light">
					<el-table :data="stus" style="width: 100%;height: 450px; overflow-y: scroll;" >
						<el-table-column prop="id" label="序号" width="80">
							
						</el-table-column>
						<el-table-column prop="id" label="学号" width="80">
						</el-table-column>
						<el-table-column prop="name" label="姓名" width="80">
						</el-table-column>
						<el-table-column prop="sex" label="性别" width="80">
						</el-table-column>
						<el-table-column prop="hobbies" label="爱好">
						</el-table-column>
						<el-table-column prop="adress" label="籍贯">
						</el-table-column>
						<el-table-column prop="beizhu" label="备注">
						</el-table-column>
						<el-table-column prop="beizhu1" label="操作">
							<template slot-scope="scope">
							<el-button type="primary" @click="update(scope.row,scope.$index)">修改</el-button>
							</template>
						</el-table-column>
						
					</el-table>


				</div>
			</el-col>
		</el-row>

		</div>

</template>

<script>
	import axios from "axios"
	export default {
		data() {
			return {
				'user': {
					'id': "1",
					'name': "bob",
					'sex': "男",
					'hobbies': [],
					'adress': "陕西省",
					'beizhu': ""
				},
				stus: [],
				index: "",
			};
		},
		methods: {
			adduser: function() {
				//定义零时变量
				//var tmp={};
				//tmp.id=this.user.id;
				this.stus.push({
					'id': this.user.id,
					'name': this.user.name,
					'sex': this.user.sex,
					'hobbies': this.user.hobbies,
					'adress': this.user.adress,
					'beizhu': this.user.beizhu
				})
			},
			remove: function(idx) {
				this.stus.splice(idx, 1)
			},
			update: function(s,index) {
				console.log(s)
				var tmp = {};
				tmp.id = s.id;
				tmp.name = s.name;
				tmp.sex = s.sex;
				tmp.hobbies = s.hobbies;
				tmp.adress = s.adress;
				tmp.beizhu = s.beizhu;
				this.user = tmp
				this.index = index

			},
			updateuser: function() {
				var tmp = {};
				tmp.id = this.user.id;
				tmp.name = this.user.name;
				tmp.sex = this.user.sex;
				tmp.hobbies = this.user.hobbies;
				tmp.adress = this.user.adress;
				tmp.beizhu = this.user.beizhu;
				this.stus.splice(this.index, 1, tmp)

			}
			
		}

	}
</script>
