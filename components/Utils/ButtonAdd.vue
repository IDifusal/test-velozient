<template>
  <div>
    <div
    @click="openModal"
      class="
        button-add
        absolute
        w-16
        h-16
        rounded-full
        place-items-center
        flex
        justify-center
      "
    >
      <svg width="32" height="32" viewBox="0 0 24 24">
        <path fill="#FFFFFF " d="M19 13h-6v6h-2v-6H5v-2h6V5h2v6h6v2Z" />
      </svg>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    openModal(){
      this.$emit('openModal')
    }
  },
}
</script>
<style lang="scss" scoped>
.button-add {
  background: rgb(192, 62, 55);
  bottom: 50px;
  right: 50px;
  &:hover {
    cursor: pointer;
    transition: 0.5s all ease 0s;
    box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
    bottom: 60px;
  }
}
</style>