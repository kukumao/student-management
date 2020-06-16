<template>
  <div class="main">
    <el-form :model="form" ref="form" :rules="formRules" label-width="150px">
      <template v-for="item in form.skuPriceList">
        <input-item :key="item.customerTypeName" :propItem="item" :inputValue="item.price" @componentInit="componentInitHandler" @componentBlur="componentBlurHandler"></input-item>
      </template>
    </el-form>
    <el-form-item>
      <el-button type="primary" @click="sure">保存</el-button>
    </el-form-item>
  </div>
</template>
<script>
import InputItem from './inputItem';

export default {
  components: { InputItem },
  data() {
    return {
      form: {
        skuPriceList: []
      },
      formRules: {}
    };
  },
  methods: {
    //组件初始化
    componentInitHandler(id, list) {
      this.formRules['item' + id] = list;
    },
    componentBlurHandler(id, val) {
      this.form['item' + id] = val;
    },
    cancel() {
      this.$emit('closePriceDialog', '关闭弹框');
    },
    sure() {
      this.$refs['form'].validate(valid => {
        if (valid) {
          let skuPriceList = [];
          this.form.skuPriceList.forEach(item => {
            skuPriceList.push({
              customerType: item.customerType,
              price: this.form['item' + item.id]
            });
          });
          let pm = {
            marketPrice: this.form.marketPrice,
            costPrice: this.form.costPrice,
            purchasePrice: this.form.purchasePrice,
            isSynchronous: this.priceSetting, //设置价格为true，预约改价为false
            skuPriceList: skuPriceList
          };
          ProductModel.updateSkuShopPrice(pm).then(res => {
            if (res.code == 200) {
              this.$message.success('设置成功');
              this.$emit('closePriceDialog', '关闭弹框');
            } else if (res.detail) {
              this.$message.error(res.detail);
            } else {
              this.$message.error('设置失败');
            }
          });
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
