<template>
  <div @mouseover="actions = true" @mouseleave="actions =false" class="card-item">
    <div
      class="card-image h-20 place-items-center flex justify-center relative"
    >
      <svg width="32" height="32" viewBox="0 0 24 24">
        <path
          fill="currentColor"
          d="M12 12h7c-.53 4.11-3.28 7.78-7 8.92V12H5V6.3l7-3.11M12 1L3 5v6c0 5.55 3.84 10.73 9 12c5.16-1.27 9-6.45 9-12V5l-9-4Z"
        />
      </svg>
      <div class="card-overlay absolute">
        <div
          @click="copyLink(item.url)"
          class="
            flex
            w-full
            h-full
            place-items-center
            justify-center
            cursor-pointer
            text-white
          "
        >
          Copylink
        </div>
      </div>
    </div>
    <div class="card-footer p-2 capitalize grid">
      <div>
        <div class="card-footer__title">
          {{ item.name }}
        </div>
        <div class="card-footer__subtitle text-xs">
          {{ item.username }}
        </div>
      </div>
      <div v-show="actions" class="card-footer__actions place-items-center flex justify-center">
        <div @click="editItem" class="card-action" data-tooltip="Edit">
          <svg width="18" height="18" viewBox="0 0 24 24">
            <path
              fill="currentColor"
              d="M5 3c-1.11 0-2 .89-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7h-2v7H5V5h7V3H5m12.78 1a.69.69 0 0 0-.48.2l-1.22 1.21l2.5 2.5L19.8 6.7c.26-.26.26-.7 0-.95L18.25 4.2c-.13-.13-.3-.2-.47-.2m-2.41 2.12L8 13.5V16h2.5l7.37-7.38l-2.5-2.5Z"
            />
          </svg>
        </div>
        <div @click="deleteItem" class="card-action" data-tooltip="Delete">
          <svg width="18" height="18" viewBox="0 0 24 24">
            <path
              fill="currentColor"
              d="M6 19a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2V7H6v12m2.46-7.12l1.41-1.41L12 12.59l2.12-2.12l1.41 1.41L13.41 14l2.12 2.12l-1.41 1.41L12 15.41l-2.12 2.12l-1.41-1.41L10.59 14l-2.13-2.12M15.5 4l-1-1h-5l-1 1H5v2h14V4h-3.5Z"
            />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    item: {
      type: Object,
      default: () => {},
    },
    index:{
      type:Number,
      default:-1
    }
  },
  data() {
    return {
      actions:false
    }
  },
  methods: {
    copyLink(url) {
      navigator.clipboard.writeText(url);
      setTimeout(() => {
        alert("Link copied to clipboard!");
      }, 10);
    },
    editItem(){
      this.$emit('editItem',this.item)
    },
    deleteItem(){
      this.$emit('deleteItem',this.item,this.index)
    }
  },
};
</script>
<style lang="scss" scoped>
.card {
  &-item {
    border-radius: 2px;
    box-shadow: 0 1px 3px RGBA(0, 24, 48, 0.2);
    display: inline-block;
    background-color: #fff;
    position: relative;
    vertical-align: top;
  }
  &-overlay {
    z-index: 9;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.6);
    visibility: hidden;
  }
  &-footer {
    grid-template-columns: 70% 30%;
  }
}
.card-image:hover > .card-overlay {
  visibility: visible !important;
}
</style>