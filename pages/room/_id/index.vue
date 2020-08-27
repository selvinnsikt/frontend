<template>
  <div class="main-content">
    <h1 class="title is-2">
      Velkommen
      <span id="name">{{ name }}</span>
    </h1>
    <p>Kopier denne koden og gi til vennene dine</p>
    <b-field id="roomInput">
      <b-input
        size="is-large"
        readonly="true"
        :value="roomId"
        v-model="roomId"
      ></b-input>
    </b-field>

    <b-button
      @click="toggleReady"
      size="is-large"
      :icon-left="readyButtonIcon"
      :type="readyButtonColor"
      inverted
      >{{ readyButtonText }}</b-button
    >
  </div>
</template>

<script>
export default {
  name: "RoomId",
  data: function () {
    return {
      roomId: this.$route.params.id,
      name: this.$route.query.name,
      ready: false,
    };
  },
  computed: {
    readyButtonIcon: function () {
      return this.ready ? "cancel" : "check";
    },
    readyButtonText: function () {
      return this.ready ? "Avbryt" : "Klar?";
    },
    readyButtonColor: function () {
      return this.ready ? "is-danger" : "is-primary";
    },
  },
  methods: {
    toggleReady: function () {
      this.ready = !this.ready;
    },
  },
};
</script>
<style lang="scss" scoped>
.main-content {
  margin: 2em auto;
  width: 50%;
}
#roomInput {
  margin-top: 1em;
  width: 7rem;
}
#name {
  text-decoration: underline;
  text-decoration-skip-ink: auto;
  color: white;
}
</style>
