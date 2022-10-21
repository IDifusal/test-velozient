<template>
  <div class="modal w-screen h-screen place-items-center flex justify-center">
    <div class="modal-content w-5/12 h-2/5">
      <div
        class="modal-content__header flex justify-between text-white px-3 py-4"
      >
        <svg
          @click="closeModal"
          class="cursor-pointer"
          width="25"
          height="25"
          viewBox="0 0 24 24"
        >
          <path
            fill="currentColor"
            d="M20 11v2H8l5.5 5.5l-1.42 1.42L4.16 12l7.92-7.92L13.5 5.5L8 11h12Z"
          />
        </svg>
        <h2 class="text-base">
          {{ title }}
        </h2>
        <svg
          @click="closeModal"
          class="cursor-pointer"
          width="25"
          height="25"
          viewBox="0 0 24 24"
        >
          <path
            fill="currentColor"
            d="M19 6.41L17.59 5L12 10.59L6.41 5L5 6.41L10.59 12L5 17.59L6.41 19L12 13.41L17.59 19L19 17.59L13.41 12L19 6.41Z"
          />
        </svg>
      </div>
      <div class="modal-content__form">
        <div>
          <label for="url">Url:</label>
          <input
            v-model="form.url"
            type="text"
            name="url"
            class="form-control"
          />
          <div v-if="errorUrl" class="text-red-600 text-xs mt-1">
            Required Field
          </div>
          <div class="md:flex gap-4">
            <div class="w-1/2 md:w-full">
              <label for="url">Name:</label>
              <input
                v-model="form.name"
                type="text"
                name="name"
                class="form-control"
              />
              <div v-if="errorName" class="text-red-600 text-xs mt-1">
                Required Field
              </div>
            </div>
            <div class="w-1/2 md:w-full">
              <label for="url">Username:</label>
              <input
                v-model="form.username"
                type="text"
                name="username"
                class="form-control"
              />
              <div v-if="errorUsername" class="text-red-600 text-xs mt-1">
                Required Field
              </div>
            </div>
          </div>
          <div class="modal-password relative">
            <label for="url">Password:</label>
            <input
              :type="showPassword ? 'text' : 'password'"
              v-model="form.password"
              name="passowrd"
              class="form-control"
            />
            <div v-if="errorPassword" class="text-red-600 text-xs mt-1">
              Required Field
            </div>
            <div v-if="form.password.length > 0">
              <div
                v-if="showPassword"
                class="svg-pass absolute top-[26px] right-0"
              >
                <svg
                  @click="showPassword = !showPassword"
                  class="cursor-pointer"
                  width="25"
                  height="25"
                  viewBox="0 0 24 24"
                >
                  <path
                    fill="currentColor"
                    d="M2 5.27L3.28 4L20 20.72L18.73 22l-3.08-3.08c-1.15.38-2.37.58-3.65.58c-5 0-9.27-3.11-11-7.5c.69-1.76 1.79-3.31 3.19-4.54L2 5.27M12 9a3 3 0 0 1 3 3a3 3 0 0 1-.17 1L11 9.17A3 3 0 0 1 12 9m0-4.5c5 0 9.27 3.11 11 7.5a11.79 11.79 0 0 1-4 5.19l-1.42-1.43A9.862 9.862 0 0 0 20.82 12A9.821 9.821 0 0 0 12 6.5c-1.09 0-2.16.18-3.16.5L7.3 5.47c1.44-.62 3.03-.97 4.7-.97M3.18 12A9.821 9.821 0 0 0 12 17.5c.69 0 1.37-.07 2-.21L11.72 15A3.064 3.064 0 0 1 9 12.28L5.6 8.87c-.99.85-1.82 1.91-2.42 3.13Z"
                  />
                </svg>
              </div>
              <div v-else class="svg-pass absolute top-[26px] right-0">
                <svg
                  @click="showPassword = !showPassword"
                  class="cursor-pointer"
                  width="25"
                  height="25"
                  viewBox="0 0 24 24"
                >
                  <path
                    fill="currentColor"
                    d="M12 9a3 3 0 0 0-3 3a3 3 0 0 0 3 3a3 3 0 0 0 3-3a3 3 0 0 0-3-3m0 8a5 5 0 0 1-5-5a5 5 0 0 1 5-5a5 5 0 0 1 5 5a5 5 0 0 1-5 5m0-12.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5Z"
                  />
                </svg>
              </div>
            </div>
          </div>
        </div>
        <div class="modal-actions flex gap-4 justify-end">
          <ButtonCustom
            @clickEvent="closeModal"
            text="Cancelar"
            color="white"
          />
          <ButtonCustom @clickEvent="saveItem" text="Save" color="red" />
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import ButtonCustom from "@/components/Utils/Button.vue";
export default {
  components: {
    ButtonCustom,
  },
  props: {
    title: {
      type: String,
      default: "",
    },
    activeItem: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {
      showPassword: false,
      form: {
        url: "",
        name: "",
        username: "",
        password: "",
      },
      errorUrl: false,
      errorName: false,
      errorUsername: false,
      errorPassword: false,
    };
  },
  mounted() {
    if (this.$attrs.item) {
      this.form = this.$attrs.item;
    }
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
    saveItem() {
      if (this.form.url.length == 0) {
        this.errorUrl = true;
        return;
      } else {
        this.errorUrl = false;
      }
      if (this.form.name.length == 0) {
        this.errorName = true;
        return;
      } else {
        this.errorName = false;
      }
      if (this.form.username.length == 0) {
        this.errorUsername = true;
        return;
      } else {
        this.errorUsername = false;
      }
      if (this.form.password.length == 0) {
        this.errorPassword = true;
        return;
      } else {
        this.errorPassword = false;
      }
      this.$emit("saveItem", this.form);
      this.form = {
        url: "",
        name: "",
        username: "",
        password: "",
      };
    },
  },
};
</script>
<style lang="scss" scoped>
.modal {
  background: rgba(52, 61, 68, 0.6);
  position: fixed;
  top: 0px !important;
  left: 0;
  &-content {
    background: rgb(240, 241, 242);
    &__header {
      background: rgb(192, 62, 55);
    }
    &__form {
      padding: 20px;
    }
  }
}
.form-control {
  font-size: 16px;
  height: 30px;
  padding: 0 5px 0 5px;
  border-width: 1px;
  border-style: solid;
  border-color: #a7afba;
  box-sizing: border-box;
  width: 100%;
  color: #000;
  background-color: #fff;
  margin-bottom: 10px;
}
.modal-content__form {
  justify-content: space-between;
  padding: 20px;
  height: 84%;
  display: flex;
  flex-direction: column;
}
</style>