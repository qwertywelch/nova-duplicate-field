<template>
  <a
    href
    @click.prevent="onClick"
    title="Duplicate"
    class="cursor-pointer text-70 hover:text-primary no-underline flex items-center"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      width="24"
      height="24"
      class="fill-current"
    >
      <path
        d="M17 7h2.25c.97 0 1.75.78 1.75 1.75v10.5c0 .97-.78 1.75-1.75 1.75H8.75C7.78 21 7 20.22 7 19.25V17H4.75C3.78 17 3 16.22 3 15.25V4.75C3 3.78 3.78 3 4.75 3h10.5c.97 0 1.75.78 1.75 1.75V7zm-2 0V5H5v10h2V8.75C7 7.78 7.78 7 8.75 7H15zM9 9v10h10V9H9z"
      ></path>
    </svg>

    <span v-if="this.field.showText">- Duplicate</span>
  </a>
</template>

<script>
import axios from "axios";

export default {
  props: ["resourceName", "field"],

  methods: {
    onClick() {
      axios
        .post("/nova-vendor/jackabox/nova-duplicate", {
          model: this.field.model ? this.field.model : "",
          id: this.field.id ? this.field.id : "",
          resource: this.field.resource ? this.field.resource : "",
          relations: this.field.relations ? this.field.relations : "",
          except: this.field.except ? this.field.except : "",
          override: this.field.override ? this.field.override : ""
        })
        .then(response => {
          window.location.replace(response.data.destination);
        })
        .catch(error => {
          console.log(error);
        });
    }
  },

  mounted() {
    let parentElement = this.$el.parentElement;
    parentElement.classList.add("td-fit");
    parentElement.style.paddingRight = "0px";
  }
};
</script>
