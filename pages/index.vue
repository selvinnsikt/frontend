<template>
  <section>
    <b-loading
      :active="isLoading"
      :is-full-page="true"
      :can-cancel="false"
    ></b-loading>
    <div class="grid-container">
      <div class="columns">
        <div class="column">
          <h1 class="title is-1">Selvinnsikt</h1>
        </div>
      </div>

      <div class="columns">
        <div class="column">
          <b-field
            :type="nameInputType"
            :message="nameInputMessage"
            label="Navn:"
            class="inputField"
          >
            <b-input
              @focus="resetNameInputValidation"
              size="is-large"
              v-model="name"
            ></b-input>
          </b-field>
          <hr class="dividerNoText" />
          <b-button
            id="create"
            size="is-large"
            type="is-primary"
            inverted
            outlined
            @click="createRoom"
            >Lag Rom</b-button
          >
          <div class="divider">OR</div>
          <b-field label="Rom ID:" class="inputField">
            <b-input size="is-large"></b-input>
          </b-field>
          <b-button
            id="join"
            size="is-large"
            type="is-primary"
            inverted
            @click="joinRoom"
            >Bli med</b-button
          >
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Card from "~/components/Card";

export default {
  name: "HomePage",

  components: {
    Card,
  },
  data: function () {
    return {
      socket: undefined,
      isLoading: false,
      name: "",
      nameInputType: "",
      nameInputMessage: "",
    };
  },
  methods: {
    resetNameInputValidation() {
      this.nameInputType = "";
      this.nameInputMessage = "";
    },
    isEmptyOrSpaces(str) {
      return str === null || str.match(/^ *$/) !== null;
    },
    joinRoom() {
      if (this.isEmptyOrSpaces(this.name)) {
        this.nameInputType = "is-danger";
        this.nameInputMessage = "Navn påkrevd";
        return;
      }
      //this.isLoading = true;
      //let socket = new WebSocket("ws://localhost:8080/join/");
    },
    createRoom() {
      if (this.isEmptyOrSpaces(this.name)) {
        this.nameInputType = "is-danger";
        this.nameInputMessage = "Navn påkrevd";
        return;
      }
      this.isLoading = true;
      this.$axios
        .$get("/create")
        .then((res) => {
          console.log(res);
          this.isLoading = false;
          this.$router.push("/room/" + res.hub + "?name=" + this.name);
        })
        .catch((err) => {
          console.log(err);
          this.isLoading = false;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~bulma";
@import "~buefy/src/scss/buefy";
@import "~@creativebulma/bulma-divider";

h1 {
  text-align: center;
  margin-top: 2em;
}

.grid-container {
  margin: 0 auto;
}
button {
  display: block;
  margin: 1.5em auto;
}
#create {
  width: 8em;
  display: block;
}
#join {
  width: 10em;
  display: block;
}
.inputField {
  width: 12em;
  margin: 0 auto;
}
.dividerNoText {
  border: 0;
  height: 1px;
  background: #333;
  background-image: linear-gradient(to right, $primary, $border, $primary);
}
</style>
