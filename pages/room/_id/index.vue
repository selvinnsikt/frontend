<template>
  <div>
    <h1 class="title is-2">Velkommen {{name}}</h1>
    <h1 class="title is-3">Venter på deltakere</h1>
    {{roomId}}
  </div>
</template>

<script>
export default {
  name: "RoomId",
  data: function () {
    return {
      roomId: this.$route.params.id,
      name: this.$route.query.name,
    };
  },
};
</script>

<style>
</style>