<template>
  <li>
    <h2>{{ name }} {{ isFavourite ? " (Favourite)" : "" }}</h2>
    <button @click="toggleFavourite">Toggle Favourite</button>
    <button @click="toggleDetails">{{ buttonDetails }} Details</button>
    <ul v-if="detailsVisible">
      <li><strong>Phone:</strong> {{ phoneNumber }}</li>
      <li><strong>Email:</strong> {{ emailAddress }}</li>
    </ul>
  </li>
</template>

<script>
export default {
  //   props: ["name", "phoneNumber", "emailAddress"],
  mounted() {
    console.log(this.$props);
  },
  props: {
    id: {
      type: Number,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    phoneNumber: {
      type: Number,
      required: true,
    },
    emailAddress: {
      type: String,
      required: true,
    },
    isFavourite: {
      type: Boolean,
      required: true,
    },
  },
  // emits: ["toggle-favourite"],
  emits: {
    "toggle-favourite": function (id) {
      if (id) {
        return true;
      } else {
        console.warn("id is missing ");
        return false;
      }
    },
  },
  data() {
    return {
      detailsVisible: false,
      friend: {
        id: 1,
        name: "Abhishek Aryan",
        phone: 123344444,
        email: "send2abhishek@liv.com",
      },
    };
  },
  computed: {
    buttonDetails() {
      return this.detailsVisible ? "Hide" : "Show";
    },
  },
  methods: {
    toggleDetails() {
      this.detailsVisible = !this.detailsVisible;
    },
    toggleFavourite() {
      this.$emit("toggle-favourite", this.id);
    },
  },
};
</script>