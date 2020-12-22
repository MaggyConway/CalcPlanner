<template>
	<el-container>
	<el-header height="40px">
		<el-row :gutter="20">
			<el-col :span="10">
				<div class="sign-in">
					<el-form :inline="true" size="mini" ref="form" :model="form">
						<el-form-item>
							<el-input v-model="form.name" class="sign-in--input" placeholder="Логин"></el-input>
						</el-form-item>
						<el-form-item prop="pass">
							<el-input type="password" v-model="ruleForm.pass" autocomplete="off" placeholder="Пароль"></el-input>
						</el-form-item>
						<el-form-item>
							<el-button round @click="submitForm('ruleForm')">Войти</el-button>
						</el-form-item>
					</el-form>
				</div>
			</el-col>
			<el-col :span="14">
				<!-- <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
					<el-menu-item index="1">Главная</el-menu-item>
					<el-menu-item index="2">Профиль</el-menu-item>
					<el-menu-item index="3">Настройки</el-menu-item>
				</el-menu> -->

				<!-- <ul class="menu">
					<li><a href="#">Главная</a></li>
					<li><a href="#">Профиль</a></li>
					<li><a href="#">Настройки</a></li>
				</ul> -->
			</el-col>
		</el-row>


	</el-header>
	<el-main>
		<el-row :gutter="20">
			<el-col :span="8">
				<div class="grid-content first-block">
					<el-date-picker
						v-model="value1"
						type="date"
						placeholder="Pick a day">
					</el-date-picker>

					<el-button @click="visible = true" class="openModalBtn">Open Modal</el-button>
					<el-dialog :visible.sync="visible" title="Hello world">
						<p>Try Element</p>
					</el-dialog>
				</div>
			</el-col>
			<el-col :span="8"><div class="grid-content bg-purple-dark"></div></el-col>
			<el-col :span="8"><div class="grid-content bg-purple-dark"></div></el-col>
		</el-row>
	</el-main>
	</el-container>
</template>

<script>
export default {
	data: function() {
		var validatePass = (rule, value, callback) => {
			if (value === '') {
				callback(new Error('Please input the password'));
			} else {
				if (this.ruleForm.checkPass !== '') {
					this.$refs.ruleForm.validateField('checkPass');
				}
				callback();
			}
		};

		return {
			// activeIndex: '1',
			ruleForm: {
				pass: '',
			},
			rules: {
				pass: [
					{ validator: validatePass, trigger: 'blur' }
				],
			},

			visible: false,
			pickerOptions: {
				disabledDate(time) {
					return time.getTime() > Date.now();
				},
			shortcuts: [
				{
					text: 'Today',
					onClick(picker) {
						picker.$emit('pick', new Date());
					}
				}, {
					text: 'Yesterday',
					onClick(picker) {
					const date = new Date();
					date.setTime(date.getTime() - 3600 * 1000 * 24);
					picker.$emit('pick', date);
				}
				}, {
					text: 'A week ago',
					onClick(picker) {
						const date = new Date();
						date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
						picker.$emit('pick', date);
					}
				}]
			},
			value1: '',
			form: {
				name: '',
			}
		}
	},
	methods: {
		submitForm(formName) {
			this.$refs[formName].validate((valid) => {
				if (valid) {
				alert('submit!');
				} else {
				console.log('error submit!!');
				return false;
				}
			});
		},
		// handleSelect(key, keyPath) {
		// 	console.log(key, keyPath);
      // }
	}
}
</script>

<style>
	.el-header {
		background-color: #5f8aff;
		color: rgb(255, 255, 255);
		text-align: center;
		margin-bottom: 20px;
	}
	.grid-content {
		border-radius: 15px;
		min-height: 250px;
		padding: 15px;
		position: relative;
	}
	/* .el-row {
		margin-left: -10px;
		margin-right: -10px;
	} */
	.el-col {
		border-radius: 4px;
	}
	.bg-purple-dark {
		background: #99a9bf;
	}
	.openModalBtn {
		margin-top: 25px;
		display: block;
	}
	.first-block {
		border: 3px solid #99a9bf;
		display: flex;
		-webkit-flex-direction: column;
		-ms-flex-direction: column;
		flex-direction: column;
		-webkit-justify-content: flex-start;
		justify-content: flex-start;
		-webkit-align-items: center;
		align-items: center;
	}
	.sign-in {
		display: flex;
		-webkit-flex-direction: row;
		-ms-flex-direction: row;
		flex-direction: row;
		-webkit-justify-content: flex-start;
		justify-content: flex-start;
		-webkit-align-items: center;
		align-items: center;
		height: 38px;
	}
	.el-input--mini .el-input__inner {
		-webkit-border-radius: 20px;
		border-radius: 20px;
	}
	.el-form-item.el-form-item--mini {
		margin-bottom: 0;
	}
</style>