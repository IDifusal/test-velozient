<template>
  <div>
    <TopBar @searchInput="searchInput" />
    <div class="content">
      <h2 class="text-1xl font-bold">Passwords</h2>
      <div class="list-cards grid">
        <div v-if="itemsFiltered.length> 0">
          <ListCards
            @saveItem="saveItem"
            @deleteItem="deleteItem"
            :listItems="itemsFiltered"
          ></ListCards>
        </div>
        <div v-else-if="searchText != ''">
          <EmptySearch/>
        </div>
        <ButtonAdd @openModal="openModal" />
        <Modal
          v-if="modal"
          @saveItem="saveItem"
          @closeModal="closeModal"
          title="Add password"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ListCards from "@/components/Home/ListCards.vue";
import ButtonAdd from "@/components/Utils/ButtonAdd.vue";
import Modal from "@/components/Utils/Modal.vue";
import TopBar from "@/components/UI/Topbar.vue";
import EmptySearch from "@/components/UI/EmptySearch"

export default {
  name: "IndexPage",
  components: {
    ListCards,
    ButtonAdd,
    Modal,
    TopBar,
    EmptySearch
  },
  data() {
    return {
      modal: false,
      searchText: "",
      items: [
        {
          url: "https://www.google.com/",
          name: "Google",
          username: "admin",
          password: "root",
        },
        {
          url: "https://youtube.com/",
          name: "Youtube",
          username: "username2",
          password: "password",
        },
      ],
      itemsFiltered: [],
    };
  },
  mounted() {
    this.itemsFiltered = this.items;
  },
  methods: {
    closeModal() {
      this.modal = false;
    },
    openModal() {
      this.modal = true;
    },
    saveItem(item) {
      let findItem = this.items.find((x) => x.url == item.url);
      if (findItem) {
        findItem = item;
        alert("Updated!");
      } else {
        this.items.push(item);
      }
      this.modal = false;
    },
    deleteItem(item, index) {
      this.items.splice(index, 1);
    },
    searchInput(text) {
      this.searchText = text;
      let textToFind= text.toLowerCase()
      this.itemsFiltered = this.items.filter((x) => {
        return (
          x.name.toLowerCase().includes(textToFind)
        );
      });
    },
  },
};
</script>
<style>
.content {
  padding: 12px 48px;
}
</style>
