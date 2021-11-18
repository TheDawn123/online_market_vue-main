<template>
  <el-container>
    <el-header>
      <Userdetail></Userdetail>
    </el-header>
    <el-container>
      <el-aside width="180px" >
        <Custside></Custside>
      </el-aside>
      <el-main>
        <el-table :data="goods" stripe border style="width:100%" highlight-current-row>
          <el-table-column prop="gid" label="商品名称" align="center" min-width="120"></el-table-column>
          <el-table-column prop="gname" label="商品价格" align="center" min-width="100"></el-table-column>
          <el-table-column prop="price" label="交易时间" align="center" min-width="120"></el-table-column>
          <el-table-column prop="status" label="交易地点" align="center" min-width="100"></el-table-column>
          <el-table-column prop="result" label="交易结果" align="center" min-width="100"></el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
import Userdetail from "@/components/Userdetail";
import Custside from "@/components/Custside";
export default {
  name: "Custhistory",
  components:{Userdetail,Custside},
  data(){
    return{

    }
  }
}
</script>

<style scoped>

</style>
