<template>
  <el-container>
    <el-header>
      <Userdetail></Userdetail>
    </el-header>
    <el-container>
      <el-aside width="600px">
          <div class="block">
            <el-image
                style=" width: 500px; height: 450px"
                :src="url"
                fit="fill"></el-image>
          </div>
      </el-aside>
      <el-main>
        <el-form class="des">
          <el-form-item label="商品名:">{{this.good['gname']}}</el-form-item>
          <el-form-item label="商品价格:">{{this.good['price']}}</el-form-item>
          <el-form-item label="商品描述:">{{this.good['description']}}</el-form-item>
          <el-button v-if="good.status===0" type="primary" @click="Buy">购买</el-button>
          <el-button v-if="good.status===1" type="info">商品已冻结</el-button>
          <el-button v-if="good.status===2" type="info">商品已下架</el-button>
        </el-form>
      </el-main>
    </el-container>
  </el-container>


</template>

<script>
import Userdetail from "@/components/Userdetail";

export default {
  name: "Buy",
  components: {Userdetail},
  comments: {Userdetail},
  data() {
    return {
      url: 'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
      good : {}

    }
  },methods: {
    Buy(){
      this.$router.push({
        name: 'Buy',
        params : {
          good: this.good
        }
      })
    }
  },
  created() {
    let gid = this.$route.params.gid
    if (gid === undefined)
      gid = localStorage.getItem('gid')
    else
      localStorage.setItem('gid',gid)
    this.$axios({
      method:'get',
      url: '/good/'+gid
    }).then(res=>{
      this.good["uid"]=res.data.data.uid
      this.good["gid"]=res.data.data.gid
      this.good["gname"]=res.data.data.gname
      this.good["image"]=res.data.data.image
      this.good["price"]=res.data.data.price
      this.good["stock"]=res.data.data.stock
      this.good["status"]=res.data.data.status
      this.good["description"]=res.data.data.description
      this.url = res.data.data.image
    })
  }

}


</script>

<style scoped>
.block{
  margin: 60px 60px;
}
.des{
  margin: 20px 0;
}


</style>
