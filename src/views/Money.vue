<template>
  <Layout class-prefix="layout">
    {{ record }}
    <NumberPad @update:value="onUpdateAmount" />
    <Types :value.sync="record.type" />
    <Notes @update:value="onUpdateNotes" />
    <Tags :data-source.sync="tags" @update:value="updateTags" />
  </Layout>
</template>

<script lang="ts">
import Tags from "@/components/Tags.vue";
import Notes from "@/components/Notes.vue";
import Types from "@/components/Types.vue";
import NumberPad from "@/components/NumberPad.vue";
import Vue from "vue";
import { Component, Watch } from "vue-property-decorator";

type Record = {
  tags: string[];
  notes: string[];
  type: string[];
  amount: number;
};

@Component({
  components: { Tags, Notes, Types, NumberPad },
})
export default class Money extends Vue {
  tags = ["衣", "食", "住", "行"];
  record: Record = { tags: [], notes: [], type: [], amount: 0 };

  onUpdateTags(value: string[]) {
    this.record.tags = value;
  }
  onUpdateNotes(value: string[]) {
    this.record.notes = value;
  }
  onUpdateType(value: string[]) {
    this.record.type = value;
  }
  onUpdateAmount(value: string[]) {
    this.record.amount = parseFloat(value);
  }
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>

