title:element ui 常用记录
date: 2019-9-22
Category: ui
Tags: ui,vue,element ui
Authors: openui
Summary: element ui 常用记录

### element ui

* 安装使用

  > npm i element-ui -S
  
* 引入

  > //引入下面三行
  > import ElementUI from 'element-ui';
  > import 'element-ui/lib/theme-chalk/index.css';
  > Vue.use(ElementUI);

- 导航链接

  ```
   <el-menu mode="horizontal" @select="handleSelect"> 
       <el-menu-item index="1">值守系统</el-menu-item>
       <el-menu-item index="2">常用查询系统</el-menu-item>
     <el-menu-item index="3">查询系统集成</el-menu-item>
       <el-menu-item index="4">常用链接</el-menu-item>
  </el-menu>
  
   methods: {
            handleSelect(key, keyPath) {
              console.log(key, keyPath);
            }
    }
    
    <el-menu :default-active="$route.path" ...>
  每次渲染menu都会读当前path 设置为default-active
  
  ```

  

  

- button

  ```
  <el-button>鼠标滑过/点击背景变淡</el-button>
    <el-button type="primary" plain>鼠标滑过/点击背景变深色调</el-button>
    <el-button type="success" round>圆角按钮</el-button>
  <el-button type="info" icon="el-icon-search" circle>图标按钮按钮，icon放入映入的icon图标名称</el-button>
    <el-button type="text">文字按钮</el-button>
    <el-button disabled>禁用按钮</el-button>
    <el-button size="medium">不同尺寸按钮</el-button>
    <el-button :disabled="true/false">动态禁用</el-button>
    <el-button type="primary">图标加文字按钮<i class="el-icon-upload el-icon--right"></i></el-button>
    <el-button type="primary" :loading="true">加载中按钮</el-button>
  <el-button-group>
  <el-button type="primary" icon="el-icon-arrow-left">上一页</el-button>
  <el-button type="primary">下一页<i class="el-icon-arrow-right el-icon--right"></i></el-button>
  ```



- el-table

  ```
     <el-table :data="data" border class="table" ref="multipleTable" @selection-change="handleSelectionChange">
  <el-table-column type="selection" width="55" align="center"></el-table-column>
  <el-table-column prop="name" label="姓名" sortable width="150">
  </el-table-column>
  </el-table-column>
  <el-table-column prop="personid" label="身份证号" >
  </el-table-column>
  <el-table-column prop="unitcode" label="单位" >
  </el-table-column>
  <el-table-column label="操作" width="180" align="center">
      <template slot-scope="scope">
      <el-button type="text" icon="el-icon-edit" @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
      <el-button type="text" icon="el-icon-delete" class="red" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>
  ```

- template slot-scope="scope"	

  - 通过 `Scoped slot` 可以获取到 row, column, $index 和 store（table 内部的状态管理）的数据 scope.$index, scope.row

    ```
    // 动态表格
    <el-table :data="tableData" border highlight-current-row class="tb-table"  ref="multipleTable" >
               <el-table-column fixed type="index" width="100" label="序号">
              </el-table-column>
    
               <el-table-column :label="head" v-for="(head, index) in header" :key="index" width="120">
                  <template slot-scope="scope">
                    {{scope.row[index]}} 
                  </template>
               </el-table-column>
    </el-table>
    
    //
     data() {
                return {
                  header: ['Id', 'Sta1','Sta2'],
                  tableData:[['1','a','d'],['2','b','c']]
                }
    ```



- form

  ```
  <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
    <el-form-item label="活动名称" prop="name">
      <el-input v-model="ruleForm.name"></el-input>
    </el-form-item>
    <el-form-item label="活动区域" prop="region">
      <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
        <el-option label="区域一" value="shanghai"></el-option>
        <el-option label="区域二" value="beijing"></el-option>
      </el-select>
    </el-form-item>
    <el-form-item label="活动时间" required>
      <el-col :span="11">
        <el-form-item prop="date1">
          <el-date-picker type="date" placeholder="选择日期" v-model="ruleForm.date1" style="width: 100%;"></el-date-picker>
        </el-form-item>
      </el-col>
      <el-col class="line" :span="2">-</el-col>
      <el-col :span="11">
        <el-form-item prop="date2">
          <el-time-picker type="fixed-time" placeholder="选择时间" v-model="ruleForm.date2" style="width: 100%;"></el-time-picker>
        </el-form-item>
      </el-col>
    </el-form-item>
    <el-form-item label="即时配送" prop="delivery">
    
        <el-switch v-model="state"
           active-value="1"
           inactive-value="2">
      </el-switch>
    	
      <el-switch v-model="ruleForm.delivery"  
      :active-value="1"
       :inactive-value="2"
       @change=chang($event,state)></el-switch>
    </el-form-item>
    <el-form-item label="活动性质" prop="type">
      <el-checkbox-group v-model="ruleForm.type">
        <el-checkbox label="美食/餐厅线上活动" name="type"></el-checkbox>
        <el-checkbox label="地推活动" name="type"></el-checkbox>
        <el-checkbox label="线下主题活动" name="type"></el-checkbox>
        <el-checkbox label="单纯品牌曝光" name="type"></el-checkbox>
      </el-checkbox-group>
    </el-form-item>
    <el-form-item label="特殊资源" prop="resource">
      <el-radio-group v-model="ruleForm.resource" @change="changeHandler()">
        <el-radio label="1">线上品牌商赞助</el-radio>
        <el-radio label="2">线下场地免费</el-radio>
      </el-radio-group>
    </el-form-item>
    <el-form-item label="活动形式" prop="desc">
      <el-input type="textarea" v-model="ruleForm.desc"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submitForm('ruleForm')">立即创建</el-button>
      <el-button @click="resetForm('ruleForm')">重置</el-button>
    </el-form-item>
  </el-form>
  <script>
    export default {
      data() {
        return {
          ruleForm: {
            name: '',
            region: '',
            date1: '',
            date2: '',
            delivery: false,
            type: [],
            resource: '',
            desc: ''
          },
          rules: {
            name: [
              { required: true, message: '请输入活动名称', trigger: 'blur' },
              { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
            ],
            region: [
              { required: true, message: '请选择活动区域', trigger: 'change' }
            ],
            date1: [
              { type: 'date', required: true, message: '请选择日期', trigger: 'change' }
            ],
            date2: [
              { type: 'date', required: true, message: '请选择时间', trigger: 'change' }
            ],
            type: [
              { type: 'array', required: true, message: '请至少选择一个活动性质', trigger: 'change' }
            ],
            resource: [
              { required: true, message: '请选择活动资源', trigger: 'change' }
            ],
            desc: [
              { required: true, message: '请填写活动形式', trigger: 'blur' }
            ]
          }
        };
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
        resetForm(formName) {
          this.$refs[formName].resetFields();
        }
      }
    }
  </script>
  
  ```

* el-dialog

  ```
  <el-dialog :visible.sync="dialogVisibleProp" :title.sync="msg2" width="600px">
        <!-- <span>这是一段信息</span> -->
        <slot></slot>
        <div slot="footer" class="dialog-footer">
          <el-button @click="hide">取 消</el-button>
          <el-button type="primary" @click="hide">确 定</el-button>
        </div>
   </el-dialog>
  ```

  

* confirm

  ```
  //confirm
  this.$confirm('确定删除?','删除确认',{
  	confirmButtonText:'OK',
  	cancelButtonText:'cancel',
  	type:'warning'
  }).then(()=>{
  	
  }).catch(()=>{
  
  });
  // message
  // dan
  import {Message} from 'element-ui';
  Vue.use(Message);
  Vue.prototype.$message = Message;
  
  this.$message({
  	showClose:true,
  	message:'update success!',
  	type:'success',//warning 
  	center:true
  });
  ```

* 布局

  * 栅格系统

```
  <el-row :gutter=24>
  <el-col :offset="3" :span="12"></el-col>
  </el-row>

```

* container 布局容器：el-container 外层布局容器
    * el-header
    * el-footer
    * el-aside
    * el-main
  
* 控件

  * icons

    ```
    <i class="el-icon-edit"></i>
    ```

  * button

    * 可取 primary success warning info danger
    * plain 是否使用素色
    * round 是否圆角

  * 级联选择 el-cascader

    ```
    <el-cascader
    	:options="options"
	v-model="selectedOption"
    	@change="handleChange"
    >
    </el-cascader>
    
    options:[
    	{
    	value:'1',
    	label:'com',
    	children:[
    		{
    			value:'3'
    			label:'t'
    		},
    		{
    			value:'4'
    			label:'y'
    		}
    	]
    	},
    	{
    	
    	}
    ]
    ```
    
  * TimePicker
  
    ```
    <el-time-select
    	v-model="value1"
    	:picker-options="{
    		start:'09:30',
    		step:'00:15',
    		end:'18:30'
    	}"
    placeholder="选择时间"
    ></el-time-select>
    ```
    
  * DatePicker:  type类型：date week datetime
  
    ```
    <el-date-picker
    	type="date"
    >
    </el-date-picker>
    ```
  
    
  
  * Carousel 走马灯
  
    ```
    <el-carsousel>
    	<el-carsousel-item v-for="item in 4" :key="index">
    		{{item}}
    	</el-carsousel-item>
    </el-carsousel>
    ```
  
    
  
  * Collapse 折叠面板  el-collapse-item 需要title属性
  
    ```
    <el-collapse-item title="idea">
    	<div>idea is best ide</div>
    </el-collapse-item>
    ```
  
    
  
  * navigation
  
    * el-menu
  
      * el-submenu
      * el-menu-item
  
    * el-tabs
  
      ```
      <el-tabs v-model="">
      	<el-tab-pan label="用户" name="first">
      		用户信息
      	</el-tab-pan>
      </el-tabs>
      ```
  
  * Tree
  
    ```
    <el-tree
    	:data="data"
    	:props="defaultprops"
    	@node-click="handleClick"
    >
    </el-tree>
    ```
  
  * Pagination 
  
    ```
    <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="[5, 10, 20, 40]" //这是下拉框可以选择的，每选择一行，要展示多少内容
        :page-size="pagesize"         //显示当前行的条数
        layout="total, sizes, prev, pager, next, jumper"
        :total="userList.length">    //这是显示总共有多少数据，
    </el-pagination>
    
    //
     methods: {
            // 初始页currentPage、初始每页数据数pagesize和数据data
            handleSizeChange: function (size) {
                    this.pagesize = size;
                    console.log(this.pagesize)  //每页下拉显示数据
            },
            handleCurrentChange: function(currentPage){
                    this.currentPage = currentPage;
                    console.log(this.currentPage)  //点击第几页
            },
            handleUserList() {
                this.$http.get('http://localhost:3000/userList').then(res => {  //这是从本地请求的数据接口，
                    this.userList = res.body
                })
            }
    }
    ```
  
    