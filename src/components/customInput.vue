<template>
  <label>
    {{type}}: 
    <el-input
      v-bind="$attrs"
      v-model="value"
      v-on="filteredListener"
      placeholder="请输入内容"/>
  </label>
</template>

<script>
export default {
  name: 'CustomInput',
  inheritAttrs: false,
  props: {
    type: {
      type: String,
      default: 'discount'
    },
    input: {
      type: String|Number,
      default: ''
    }
  },
  data() {
    return {
      // 标识用户的输入是否以小数点 . 结尾
      dotInTheEnd: !!this.input.match(/\.$/)
    }
  },
  computed: {
    filteredListener(){
      const filteredListener = Object.assign({}, this.$listeners)
      delete filteredListener.input
      return filteredListener
    },
    value: {
      get: function() {
        // input is always discount
        const value = this.type === 'discount' ? Number(this.input) : this.discountToPercent(this.input)
        return `${value}${this.dotInTheEnd ? '.':''}`
      },
      set: function(rawValue) {
        if(/[^\d\.]/.test(rawValue)) { return }
        this.dotInTheEnd = rawValue.match(/\.$/)
        // always emit discount
        const value = this.type === 'discount' ? Number(rawValue) : this.percentToDiscount(rawValue)
        this.$emit('input', value)
      }
    }
  },

  methods: {
    // 8.5 -> 15
    percentToDiscount(percent) {
      return (10 - percent) * 10
    },

    // 30 -> 7
    discountToPercent(discount) {
      return (100 - discount) / 10
    }
  }
}
</script>
<style >

</style>