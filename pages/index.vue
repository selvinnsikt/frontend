<template>
  <section>
    <b-loading :active="isLoading" :is-full-page="true" :can-cancel="false"></b-loading>
    <div class="grid-container">
      <div class="columns">
        <div class="column">
          <h1 class="title is-1">Selvinnsikt</h1>
        </div>
      </div>

      <div class="columns">
        <div class="column">
          <b-field :type="nameInputType" :message="nameInputMessage" label="Navn:" id="nameInput">
            <b-input @focus="resetNameInputValidation" size="is-large" v-model="name"></b-input>
          </b-field>
          <b-button
            id="create"
            size="is-large"
            type="is-primary"
            inverted
            outlined
            @click="createRoom"
          >Lag Rom</b-button>
          <b-button id="join" size="is-large" type="is-primary" inverted>Bli med</b-button>
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
      // TODO: Add some sort of loader
      console.log("room create");
    },
  },
};
</script>

<style lang="scss" scoped>
@import "~bulma";
@import "~buefy/src/scss/buefy";

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
#nameInput {
  width: 12em;
  margin: 0 auto;
}
</style>
