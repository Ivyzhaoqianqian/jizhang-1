<template>
  <Layout class-prefix="layout">
    <NumberPad />
    <Types />
    <Notes />
    <Tags :data-source.sync="tags" />
  </Layout>
</template>

<script >
import Tags from "@/components/Tags.vue";
import Notes from "@/components/Notes.vue";
import Types from "@/components/Types.vue";
import NumberPad from "@/components/NumberPad.vue";

export default {
  components: { Tags, Notes, Types, NumberPad },
  name: "Money",
  data() {
    return {
      tags: ["衣", "食", "住", "行"],
    };
  },
};
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>

