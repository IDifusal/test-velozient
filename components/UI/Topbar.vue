<template>
  <div class="navbar p-3 md:grid text-white">
    <div class="navbar-item hidden md:flex">
      <svg width="32" height="32" viewBox="0 0 24 24" class="mr-3">
        <path
          fill="currentColor"
          d="M21.86 12.5A4.313 4.313 0 0 0 19 11c0-1.95-.68-3.6-2.04-4.96C15.6 4.68 13.95 4 12 4c-1.58 0-3 .47-4.25 1.43s-2.08 2.19-2.5 3.72c-1.25.28-2.29.93-3.08 1.95S1 13.28 1 14.58c0 1.51.54 2.8 1.61 3.85C3.69 19.5 5 20 6.5 20h12c1.25 0 2.31-.44 3.19-1.31c.87-.88 1.31-1.94 1.31-3.19c0-1.15-.38-2.15-1.14-3M16.57 18L14 15.43c-.57.36-1.26.57-2 .57c-2.21 0-4-1.79-4-4s1.79-4 4-4s4 1.79 4 4c0 .74-.21 1.43-.57 2L18 16.57L16.57 18M14 12c0 1.11-.89 2-2 2s-2-.89-2-2s.9-2 2-2s2 .9 2 2Z"
        />
      </svg>
      My Secure Vault
    </div>
    <div class="navbar-item">
      <input @input="seachInput" v-model="search" type="text" placeholder="seach in my vault" class="search-input w-full" />
    </div>
    <div class="navbar-item hidden md:flex">
      <img src="~/assets/images/profile-pic.png" alt="" class="mr-2" />
      Random User
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      search:''
    }
  },
  methods: {
    seachInput(){
      this.$emit('searchInput',this.search)
    }
  },
}
</script>
<style lang="scss" scoped>
.navbar {
  background: rgb(192, 62, 55);
    grid-template-columns: 20% 60% 20%;
  &-item {
    place-items: center;
    justify-content: center;
    input {
      padding: 10px;
      color: black;
      outline: none;
      padding-left: 40px;
      background-color: rgba(255,255,255,0.2);
      background-image: url('~/assets/images/search.png');
      background-repeat: no-repeat;
      background-position: 10px center;
      &:focus-visible{
          background: #FFFFFF;
          background-image: url('~/assets/images/search-active.png');
          background-repeat: no-repeat;
      background-position: 10px center;
      }
    }
  }
}
</style>