<template>
  <div>
    <button
    @click="clickEvent"
      class="btn"
      :class="{
        'btn-red': color == 'red',
      }"
    >
      {{ text }}
    </button>
  </div>
</template>
<script>
export default {
  props: {
    color: {
      type: String,
      default: "",
    },
    text: {
      type: String,
      default: "",
    },
  },
  methods: {
    clickEvent(){
        this.$emit('clickEvent')
    }
  },
};
</script>
<style lang="scss" scoped>
.btn {
  font-size: 15px;
  border-radius: 4px;
  width: 140px;
  min-width: 140px;
  line-height: 19px !important;
  border-bottom-width: 2px;
  padding: 4px 4px 3px 4px;
  background-color: #FFFFFF;
  &-red {
    background-color: #d32d27;
    color: #fff !important;
    border-color: #af0806;
    &:hover{
        background-color: #af0806;
    border-color: #910101;
    }
  }
}
</style>