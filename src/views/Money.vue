<template>
  <Layout class-prefix="layout">
    <NumberPad :value.sync="record.amount" @submit="saveRecord" />
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
// import recordListModel from "@/models/recordListModel";
// import tagListModel from "@/models/tagListModel";
import model from "@/models/recordListModal";
import RecordItem from "@/custom";
import tagListModel from "@/models/tagListModel";

const recordList = model.fetch();
const tagList = tagListModel.fetch();

@Component({
  components: { Tags, Notes, Types, NumberPad },
})
export default class Money extends Vue {
  tags = tagList;
  recordList: RecordItem[] = JSON.parse(
    window.localStorage.getItem("recordList") || "[]"
  );
  record: RecordItem = { tags: [], notes: [], type: [], amount: 0 };

  onUpdateTags(value: string[]) {
    this.record.tags = value;
  }
  onUpdateNotes(value: string[]) {
    this.record.notes = value;
  }

  saveRecord() {
    const record2: RecordItem = JSON.parse(JSON.stringify(this.record));
    record2.createAt = new Date();
    this.recordList.push(record2);
  }

  @Watch("recordList")
  onRecordListChange() {
    window.localStorage.setItem("recordList", JSON.stringify(this.recordList));
  }
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}
</style>

