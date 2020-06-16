<template>
  <el-form-item :label="this.propItem.customerTypeName" :prop="this.propName">
    <el-input v-model="value" class="inputWidth-210" @blur="onBlurHandler"></el-input>
  </el-form-item>
</template>
<script>
export default {
  name: 'InputItem',
  props: {
    propItem: {
      type: Object,
      default: {
        id: '',
        customerTypeName: '',
        price: ''
      }
    },
    inputValue: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      value: this.inputValue,
      propName: 'item' + this.propItem.id
    };
  },
  created() {
    this.init();
  },
  methods: {
    //组件初始化
    init() {
      let propList = [];
      propList.push({
        required: true,
        message: '请输入' + this.propItem.customerTypeName,
        trigger: 'blur'
      });
      this.$emit('componentInit', this.propItem.id, propList);
    },

    //组件失焦的回调
    onBlurHandler(e) {
      let value = e.target.value;
      value = value.trim();
      this.$emit('componentBlur', this.propItem.id, value);
    }
  }
};
</script>
<style lang="scss" scoped>
.inputWidth-210 {
  width: 210px;
}
</style>
