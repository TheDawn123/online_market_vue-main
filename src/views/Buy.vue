<template>
  <el-container>
    <el-header>
      <Userdetail></Userdetail>
    </el-header>
      <h2>确认订单信息</h2>
      <span>默认交易地址:</span>
    <el-container>
      <el-main>
<!--        <el-table-->
<!--            :data="tableData"-->
<!--            style="width: 100%">-->
<!--          <el-table-column-->
<!--              prop="gname"-->
<!--              label="商品名称"-->
<!--              width="180">-->
<!--          </el-table-column>-->
<!--          <el-table-column-->
<!--              prop="price"-->
<!--              label="商品价格"-->
<!--              width="180">-->
<!--          </el-table-column>-->
<!--          <el-table-column-->
<!--              prop="stock"-->
<!--              label="商品库存">-->
<!--          </el-table-column>-->
<!--          <el-table-column-->
<!--              prop="address"-->
<!--              label="购买数量">-->
<!--            <el-input-number v-model="num" :min="1"  :max="this.tableData[0].stock" size="small"></el-input-number>-->
<!--          </el-table-column>-->
<!--          <el-table-column-->
<!--              prop="total"-->
<!--              label="总价">-->
<!--          </el-table-column>-->
<!--        </el-table>-->


        <div class="label" style="margin-top: 10px">
        <div style="display: inline;width: 150px;text-align: center">商品名称</div>
        <div style="display: inline;width: 150px;text-align: center;margin-left: 150px">单价</div>
        <div style="display: inline;width: 150px;text-align: center;margin-left: 150px">商品库存</div>
        <div style="display: inline;width: 150px;text-align: center;margin-left: 150px">购买数量</div>
        <div style="display: inline;width: 150px;text-align: center;margin-left: 150px">总价</div>
          <el-divider></el-divider>
        </div>
        <div class="label2" style="margin-top: 10px">
          <div class="detail" style="display: inline;text-align: center;">{{ this.good['gname'] }}</div>
          <div class="detail" style="display: inline;text-align: center;">{{ this.good['price'] }}</div>
          <div class="detail" style="display: inline;text-align: center;">{{ this.good['stock'] }}</div>
          <div class="detail" style="display: inline;text-align: center;">
            <el-input-number v-model="num" :min="1"  :max="this.good['stock']"  label="描述文字" size="small">12</el-input-number>
          </div>
          <div style="display: inline;text-align: center;margin-left: 110px">{{ this.num * this.good['price'] }}</div>
        </div>
        <div class="label3" style="margin-top: 10px">
          <div></div>
        </div>
        <div style="float: right;margin-top: 150px">
          <div style="margin-right: 0px">实付款:</div>
          <h2>{{ this.num * this.good['price'] }} ￥</h2>
          <br>
          <el-button type="primary" style="width: 200px;background-color: red" @click="submitForm">提交订单</el-button>
        </div>
      </el-main>

    </el-container>
  </el-container>
</template>

<script>
import Userdetail from "@/components/Userdetail";
export default {
  name: "Buy",
  components: {Userdetail},
  data() {
    return {
      num:1,
      good: {},
      // total:this.num * this.good['price']
      //   tableData:[{
      //     gname:'',
      //     price:"",
      //     stock:"",
      //     total:''
      //   }]
    }
  }, methods: {
    submitForm() {
      let data = new FormData
      var total = this.num * this.good['price']
      data.append('amount',total)
      data.append('gid',this.good['gid'])
      data.append('number',this.num)
      data.append('status',0)
      data.append('uid',this.$store.getters.getUser.uid)
      this.$axios({
        method:'put',
        url:'/v2.0/orders',
        data:data
      }).then(res=>{
        console.log(res)
      })
      this.$message({
        type:"success",
        message:"下单成功"
      })
      this.$router.push('home')
       // console.log(total)


      // this.$refs[forName].validate(valid => {
      //   if (valid) {
      //     let data = new FormData
      //     data.append('username', this.ruleForm.name)
      //     data.append('userphone', this.ruleForm.phone)
      //     data.append('useraddress', this.ruleForm.address)
      //     data.append('oid', 0)
      //     data.append('gid', this.good.gid)
      //     data.append('number', 1)
      //     data.append('amount', this.good.price)
      //     data.append('status', 0)
      //     this.$axios({
      //       method: "post",
      //       data: data,
      //       url: "/orders/insert"
      //     }).then(res => {
      //       if (res.data.code === 200) {
      //         this.$message({
      //           type: "success",
      //           message: "下单成功"
      //         })
      //         this.$router.push({//下单成功页面进行跳转
      //           name: "Gooddetail"
      //         })
      //       } else {
      //         this.$message({
      //           type: "info",
      //           message: res.data.msg
      //         })
      //       }
      //       // console.log(res.data)
      //     })
      //   } else {
      //     this.$message({
      //       type: "info",
      //       message: "格式错误"
      //     })
      //   }
      // })
    },

  },created() {
    this.good = this.$route.params['good']
    if (this.good === undefined)
      this.good = localStorage.getItem('good')
    else
      localStorage.setItem('good', this.good)
    // console.log(this.good)
    // console.log(this.$store.getters.getUser.uid)
    // this.tableData[0].gname=this.good['gname']
    // this.tableData[0].price=this.good['price']
    // this.tableData[0].stock=this.good['stock']
    // console.log(this.tableData[0].stock)
  }
}
</script>

<style scoped>
.block {
  margin: 60px 20px;
}

.des {
  margin: 20px 0;
}

.label {
  margin: 60px 0;
}
span{
  float: left;
}
.detail{
  margin-left: 150px;
}
</style>
