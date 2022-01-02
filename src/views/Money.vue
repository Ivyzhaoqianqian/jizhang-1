<template>
  <Layout class-prefix="layout">
    <NumberPad />
    <Types :xxx="333" />
    <Notes />
    <Tags />
  </Layout>
</template>

<script lang="ts">
import Tags from "@/components/Tags.vue";
import Notes from "@/components/Notes.vue";
import Types from "@/components/Types.vue";
import NumberPad from "@/components/NumberPad.vue";

export default {
  components: { Tags, Notes, Types, NumberPad },
  name: "Money",
};
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>

