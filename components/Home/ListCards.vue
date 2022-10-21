<template>
  <div class="list-cards grid">
    <Card
    v-for="(item, index) in listItems"
    @deleteItem="deleteItem"
      @editItem="editItem(index)"
      :key="index"
      :item="item"
      :index="index"
    ></Card>
    <Modal
      v-if="modal"
      @saveItem="saveItem"
      @closeModal="closeModal"
      title="Edit Password"
      :item=activeItem
    />
  </div>
</template>
<script>
import Card from "@/components/Home/Card.vue";
import Modal from "@/components/Utils/Modal.vue";

export default {
  components: {
    Card,
    Modal,
  },
  data() {
    return {
      modal :false,
      activeItem: {
        url: "",
        name: "",
        username: "",
        password: "",
      },
    };
  },
  props: {
    listItems: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    deleteItem(item, index) {
      this.$emit("deleteItem", item, index);
    },
    editItem(index) {
      this.modal=true
      this.activeItem = this.listItems[index]
      //this.$emit("editItem", item, index);
    },
    closeModal(){
      this.modal = false
    },
    openModal(){
      this.modal = true
    },
    saveItem(item){
      this.$emit('saveItem',item)
      this.modal=false
    },
  },
};
</script>
<style lang="scss" scoped>
.list-cards {
  grid-template-columns: repeat(2, 50%);
  gap: 20px;
  @media(min-width: 850px){
    grid-template-columns: repeat(4, 25%);

  }
}
</style>