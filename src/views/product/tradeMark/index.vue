<template>
  <div>
    <el-button type="primary" icon="el-icon-plus" style="margin: 10px 0"
      >添加</el-button
    >
    <!-- 表格组件 -->
    <el-table style="width: 100%" border :data="list">
      <el-table-column
        label="序号"
        prop="prop"
        width="80px"
        align="center"
        type="index"
      >
      </el-table-column>
      <el-table-column label="品牌名称" prop="tmName" width="width">
      </el-table-column>
      <el-table-column label="品牌LOGO" prop="prop" width="width">
        <template slot-scope="{ row, $index }">
          <img :src="row.logoUrl" alt="" style="width:100px;height:100px;"/>
        </template>
      </el-table-column>
      <el-table-column label="操作" prop="prop" width="width">
        <template slot-scope="scope">
          <el-button size="mini" type="warning" icon="el-icon-edit"
            >编辑</el-button
          >
          <el-button size="mini" type="danger" icon="el-icon-delete"
            >删除</el-button
          >
        </template>
      </el-table-column>
    </el-table>

    <!-- 分页器 -->
    <el-pagination
      style="margin-top: 20px; text-align: center"
      :total="total"
      :current-page="page"
      :page-size="limit"
      :page-count="7"
      :page-sizes="[3, 5, 10]"
      layout="prev,pager,next,jumper,->,sizes,total"
      @current-change="handleCurrentChange"
      @size-change="handleSizeChange"
    >
    </el-pagination>
  </div>
</template>

<script>
export default {
  name: "tradeMark",
  data() {
    return {
      page: 1,
      limit: 3,
      total: 0,
      list: [],
    };
  },
  mounted() {
    this.getPageList();
  },
  methods: {
    async getPageList() {
      const { page, limit } = this;
      let result = await this.$API.tradeMark.reqTradeMarkList(page, limit);
      if (result.code == 200) {
        this.total = result.data.total;
        this.list = result.data.records;
      }
    },
    handleCurrentChange(pager){
      this.page=pager
      this.getPageList()
    },
    handleSizeChange(limit){
      this.limit=limit
      this.getPageList()
    }
  },
};
</script>

<style>
</style>