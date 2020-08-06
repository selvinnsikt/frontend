<template>
  <section class="section hero is-fullheight">
    <div class="hero-body">
      <div class="grid-container">
        <div class="columns">
          <div class="column">
            <h1 class="title is-1">Selvinnsikt</h1>
          </div>
        </div>

        <div class="columns">
          <div class="column">
            <b-button
              id="create"
              size="is-large"
              type="is-primary"
              inverted
              outlined
              >Lag Rom</b-button
            >
            <b-button id="join" size="is-large" type="is-primary" inverted
              >Bli med</b-button
            >
          </div>
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
};
</script>

<style lang="scss" scoped>
@import "~bulma";
@import "~buefy/src/scss/buefy";

h1 {
  text-align: center;
  margin-top: -2.7em;
}

.grid-container {
  margin: 0 auto;
}
button {
  display: block;
  margin: 1.5em auto;
}
.section {
  background-color: $primary;
  height: 100%;
}
#create {
  width: 8em;
  display: block;
}
#join {
  width: 10em;
  display: block;
}
</style>
