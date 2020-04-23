<template>
  <div>
    <!-- 待办 -->
    <el-table :data="list1" style="width: 100%;padding-top: 15px;">
      <el-table-column label="待办事项" min-width="200">
        <template slot-scope="scope">
          {{ scope.row.name }}
        </template>
      </el-table-column>
      <el-table-column label="日期" width="250" align="center">
        <template slot-scope="scope">
          {{ scope.row.time }}<el-tag type="warning" style="margin-left:10px;">new</el-tag>
        </template>
      </el-table-column>
    </el-table>
    <!-- 已办 -->
    <el-table :data="list2" style="width: 100%;padding-top: 15px;">
      <el-table-column label="已办事项" min-width="200">
        <template slot-scope="scope">
          {{ scope.row.name }}
        </template>
      </el-table-column>
      <el-table-column label="日期" width="250" align="center">
        <template slot-scope="scope">
          {{ scope.row.time }}<el-tag type="success" style="margin-left:10px;">end</el-tag>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
// import { transactionList } from '@/api/remote-search'

export default {
  filters: {
    statusFilter(status) {
      const statusMap = {
        success: 'success',
        pending: 'danger'
      }
      return statusMap[status]
    },
    orderNoFilter(str) {
      return str.substring(0, 30)
    }
  },
  data() {
    return {
      list: null
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      // transactionList().then(response => {
      //   this.list = response.data.items.slice(0, 8)
      // })
      this.list1 = [
        {
          name: '张三三对系统新增反馈信息',
          time: '2020-04-13 20:38:55'
        },
        {
          name: '张三三对系统新增反馈信息',
          time: '2020-04-13 20:38:55'
        },
        {
          name: '张三三对系统新增反馈信息',
          time: '2020-04-13 20:38:55'
        }
      ]
      this.list2 = [
        {
          name: '[已处理]张三三对系统新增反馈信息',
          time: '2020-04-13 20:38:55'
        },
        {
          name: '[已处理]张三三对系统新增反馈信息',
          time: '2020-04-13 20:38:55'
        },
        {
          name: '[已处理]张三三对系统新增反馈信息',
          time: '2020-04-13 20:38:55'
        }
      ]
    }
  }
}
</script>
