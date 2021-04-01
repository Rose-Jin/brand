<template>
  <div id="app">
    <!-- 卡片区域 -->
    <div class="card">
      <div class="card-header">
        添加品牌
      </div>
      <div class="card-body">
        <!-- 行内的表单 -->
        <form class="form-inline">
          <div class="col-auto">
            <label class="sr-only" for="inlineFormInputGroup"></label>
            <div class="input-group mb-2">
              <div class="input-group-prepend">
                <div class="input-group-text">品牌名称</div>
              </div>
              <input type="text" class="form-control" v-model.trim='brand'>
            </div>
          </div>
          <div class="col-auto">
            <label class="sr-only" for="inlineFormInputGroup"></label>
            <div class="input-group mb-2">
              <div class="input-group-prepend">
                <div class="input-group-text">品牌价格</div>
              </div>
              <input type="text" class="form-control" v-model.trim='price' @keyup.enter='add'>
            </div>
          </div>
          <button @click='add' type="button" class="btn btn-primary mb-2" >添加</button>
        </form>
      </div>
    </div>

    <!-- 表格区域 -->
    <table class="table table-bordered mt-2">
      <thead>
        <tr>
          <th>#</th>
          <th>车辆名称</th>
          <th>车辆价格</th>
          <th>创建时间</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody v-if='list.length>0'>
        <tr v-for='item in list' :key='item.id'>
          <td>{{item.id}}</td>
          <td>{{item.brand}}</td>
          <td :class='{red:item.price>10  }'>{{item.price}}</td>
          <td>{{item.time}}</td>
          <td>
            <a href="#" @click.prevent='del(item.id)'>删除</a>
          </td>
        </tr>
        <tr class="footer">
          <td>统计</td>
          <td colspan="2">
            总价钱：100
          </td>
          <td colspan="2">
            平均价：100
          </td>
        </tr>
      </tbody>
      <tbody v-else>
        <tr>
          <td colspan="5" class="text-center">没有更多数据</td>
        </tr>
      </tbody>
    </table>
    <div>
      
    </div>
  </div>
</template>
<script>
// import  './style/bootstrap.css'
export default {
  data(){
    return{
      list:[
      { id: 1, brand: '奔驰S450', price: 120, time: new Date('2020-12-12') },
      { id: 2, brand: '奥迪A4', price: 30, time: new Date('2020-12-01') },
      { id: 3, brand: '五菱宏光', price: 8, time: new Date() }
      ],
      brand:'',
      price:''
    }
  },
  methods:{
    del(id){
      // console.log(id);
      // const index=this.list.findIndex(item =>item.id===id)
      // this.list.splice(index,1)
      // this.list = this.list.filter(item => item.id !== id)
      this.list=this.list.filter(item=>item.id!==id)
    },
    add(){
      // console.log(this.brand);
      if(!this.brand){
        alert('品牌不许为空')
        return
      }
      if(!this.price){
        alert('价格不许为空')
        return
      }
      this.list.unshift({id:Date.now(),brand:this.brand,price:this.price,time:new Date()})
      this.brand='',
      this.price=''
    }
  }
}
</script>

<style lang="less">
#app {
  width: 60%;
  margin: 50px auto;
  a {
    margin-right: 5px;
  }
  .footer {
    background-color: rgba(0, 0, 0, .05);
  }
  .red{
    color:red
  }
}
</style>