<template>
  <div class="main">
    <el-table
      :data="tableData"
      style="width: 60%">

      <el-table-column
        prop="date"
        label="关系运算符"
        width="100">
        <template slot-scope="scope">
          <el-select v-model="scope.row.relation" placeholder="">
              <el-option
              v-for="item in relation"
              :key="item.value"
              :label="item.label"
              :value="item.value">
              </el-option>
          </el-select>
        </template>      
      </el-table-column>

      <el-table-column
        prop="date"
        label="括号"
        width="100">
        <template slot-scope="scope">
          <el-select v-model="scope.row.bracketsLeft" placeholder="">
              <el-option
              v-for="item in brackets"
              :key="item.value"
              :label="item.label"
              :value="item.value">
              </el-option>
          </el-select>
        </template>      
      </el-table-column>

      <el-table-column
        prop="date"
        label="属性"
        width="100">
        <template slot-scope="scope">
          <el-select v-model="scope.row.fileds" placeholder="">
              <el-option
              v-for="item in fileds"
              :key="item.value"
              :label="item.label"
              :value="item.value">
              </el-option>
          </el-select>
        </template>      
      </el-table-column>

      <el-table-column
        prop="date"
        label="比较运算符"
        width="100">
        <template slot-scope="scope">
          <el-select v-model="scope.row.compare" placeholder="">
              <el-option
              v-for="item in compare"
              :key="item.value"
              :label="item.label"
              :value="item.value">
              </el-option>
          </el-select>
        </template>      
      </el-table-column>

      <el-table-column
        prop="date"
        label="数值"
        width="100">      
        <template slot-scope="scope">
          <el-input v-model="scope.row.value" placeholder=""></el-input>
        </template>      
      </el-table-column>

      <el-table-column
        prop="date"
        label="括号"
        width="100">
        <template slot-scope="scope">
          <el-select v-model="scope.row.bracketsRight" placeholder="">
              <el-option
              v-for="item in brackets"
              :key="item.value"
              :label="item.label"
              :value="item.value">
              </el-option>
          </el-select>
        </template>      
      </el-table-column>

      <el-table-column
        fixed="right"
        label="操作"
        width="120">
        <template slot-scope="scope">
          <el-button
            @click.native.prevent="appendRow(tableData)"
            type="text"
            size="small">
            增加
          </el-button>
          <el-button
            @click.native.prevent="deleteRow(scope.$index, tableData)"
            type="text"
            size="small">
            移除
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    <br>
    <br>
    <el-button type="primary" plain @click="http()">查询</el-button>
    <br>
    <br>
    <el-table
      :data="stuData"
      style="width: 30%">
      <el-table-column
        prop="id"
        label="id"
        width="100">
      </el-table-column>
      <el-table-column
        prop="stuId"
        label="学号"
        width="100">
      </el-table-column>
      <el-table-column
        prop="name"
        label="姓名"
        width="100">
      </el-table-column>
      <el-table-column
        prop="classes"
        label="班级"
        width="100">
      </el-table-column>      
    </el-table>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {

    name: "post",
    methods: {
      http() {
        axios({
          method: 'post',
          url: '/api/hello/good',
          data: this.tableData
        }).then((res) => {
          console.log(res.data.data)
          this.stuData = res.data.data
        })
      },
      deleteRow(index, rows) {
        rows.splice(index, 1);
      },
      appendRow(rows) {
        const data = {
          relation: '',
          bracketsLeft: '',
          fileds: '',
          compare: '',
          value: '',
          bracketsRight: ''
        }
        this.tableData.push(data)

        console.log(this.tableData)
      }
    },
    data() {
      return {
        relation: [{
          value: '',
          label: '--'
        },{
          value: ' and ',
          label: '并且'
        },{
          value: ' or ',
          label: '或'
        }],

        brackets: [{
          value: '',
          label: '--'
        },{
          value: '(',
          label: '('
        },{
          value: ')',
          label: ')'
        }],

        fileds: [{
          value: 'name',
          label: '姓名'
        }, {
          value: 'class',
          label: '班级'
        }, {
          value: 'stu_id',
          label: '学号'
        }],

        compare: [{
          value: '=',
          label: '='
        }, {
          value: '<',
          label: '<'
        }, {
          value: '>',
          label: '>'
        }],

        stuData: [],

        tableData: [{
          relation: '',
          bracketsLeft: '',
          fileds: '',
          compare: '',
          value: '',
          bracketsRight: ''
        }]
      }
    }
  }
</script>

<style>
  .main{
    display: flex;
  }
</style>