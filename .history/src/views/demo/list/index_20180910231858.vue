<template>
  <div class="main">
    <el-form :model="form" ref="form" :rules="formRules" label-width="150px">
      <template v-for="item in form.skuPriceList">
        <input-item :key="item.customerTypeName" :propItem="item" :inputValue="item.price" @componentInit="componentInitHandler" @componentBlur="componentBlurHandler"></input-item>
      </template>
      <el-form-item>
        <el-button type="primary" @click="sure">保存</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>
<script>
import InputItem from './inputItem';

export default {
  components: { InputItem },
  data() {
    return {
      form: {
        skuPriceList: [
          {
            id: '1',
            customerTypeName: '客户类型1',
            price: '123'
          },
          {
            id: '2',
            customerTypeName: '客户类型2',
            price: '123'
          }
        ]
      },
      formRules: {}
    };
  },
  mounted(){
   
  },
  methods: {
    //组件初始化
    componentInitHandler(id, list) {
      this.formRules['item' + id] = list;
     
    },
    componentBlurHandler(id, val) {
      this.form['item' + id] = val;
       alert("123")
    },
    sure() {
      console.log(this.form)
      this.$refs['form'].validate(valid => {
        if (valid) {
          alert('校验OK');
        } else {
          return false;
        }
      });
    }
  }
};
</script>
<style lang="scss" scoped>
.inputWidth-210 {
  width: 210px;
}
.ml-150 {
  margin-left: 150px;
}
</style>
