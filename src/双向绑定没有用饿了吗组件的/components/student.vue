<template>
	<div id="div1">
		<div style="float: left; border: solid black 1px; width: 400px; height: 350px; font-size: 25px;margin-left: 300px;margin-top: 100px;">
			<table border="1" cellspacing="0" cellpadding="0" align="center">
				<tr height="50px">
					<td width="100px">id:</td>
					<td width="300" colspan="3"><input type="text" v-model='user.id' />
					</td>

				</tr>
				<tr height="50px">
					<td>name:</td>
					<td colspan="3"><input type="text" v-model='user.name' /></td>

				</tr>
				<tr height="50px">
					<td>sex:</td>
					<td><input type="radio" name="sex" value="男" v-model='user.sex' />男</td>
					<td colspan="2"><input type="radio" name="sex" value="女" v-model='user.sex' />女</td>

				</tr>
				<tr height="50px">
					<td>hobby:</td>
					<td><input type="checkbox" name="hobby" value="sing" v-model='user.hobbies' />sing</td>
					<td><input type="checkbox" name="hobby" value="run" v-model='user.hobbies' />run</td>
					<td><input type="checkbox" name="hobby" value="play" v-model='user.hobbies' />play</td>
				</tr>
				<tr height="50px">
					<td>籍贯:</td>
					<td colspan="3"><select name="adress" v-model="user.adress">
							<option>--请选择--</option>
							<option>陕西省</option>
							<option>湖南省</option>
							<option>广东省</option>
						</select></td>

				</tr>
				<tr height="50px">
					<td>备注:</td>
					<td colspan="3">
						<textarea name="beizhu" v-model='user.beizhu'></textarea></td>

				</tr>
				<tr height="50px">
					<td align="center" colspan="4">
						<button type="button" @click="adduser">添加</button>
						<button type="button" @click="updateuser(user)">修改</button>
					</td>
				</tr>
			</table>

		</div>
		<div style="float: left; border: solid black 1px; width: 700px; height: 350px;margin-left: 50px;margin-top: 100px;overflow: scroll;overflow-x: hidden;">
			<table border="1" cellspacing="0" cellpadding="0" width="100%">
				<tr height="50px">
					<th width="50px">序号</th>
					<th width="50px">学号</th>
					<th width="50px">姓名</th>
					<th width="50px">性别</th>
					<th width="200px">兴趣</th>
					<th width="50px">籍贯</th>
					<th width="200px">备注</th>
					<th width="50px">操作</th>
				</tr>
				<tr height="50px" v-for="(s,index) in stus">
					<td>{{index+1}}</td>
					<td>{{s.id}}</td>
					<td>{{s.name}}</td>
					<td>{{s.sex}}</td>
					<td>{{s.hobbies}}</td>
					<td>{{s.adress}}</td>
					<td>{{s.beizhu}}</td>
					<td><button type="button" @click="remove(index)">remove</button>
						<button type="button" @click="update(s,index)">update </button>
					</td>
				</tr>


			</table>

		</div>
	
		<button  type="button" @click="poststu">post获取</button>
		
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
			update: function(s, index) {
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

			},
			poststu:function () {
                var data={}
                data.no="999"
                //"login.jsp?no=009"
                axios.post("/web/login.jsp",data).then(function (result) {
                    console.log(result);
                    console.log(this);
                    

                });
            }





		}

	}
</script>
