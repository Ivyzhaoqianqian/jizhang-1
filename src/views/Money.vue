<template>
  <Layout class-prefix="layout">
    <NumberPad :value.sync="record.amount" @submit="saveRecord" />
    <Types :value.sync="record.type" />
    <FormItem
      fieldName="备注"
      placeholder="在这里输入备注"
      @update:value="onUpdateNotes"
    />
    <Tags :data-source.sync="tags" @update:value="updateTags" />
  </Layout>
</template>

<script lang="ts">
import Tags from "@/components/Tags.vue";
import FormItem from "@/components/FormItem.vue";
import Types from "@/components/Types.vue";
import NumberPad from "@/components/NumberPad.vue";
import Vue from "vue";
import { Component, Watch } from "vue-property-decorator";
import recordListModel from "@/models/recordListModel";
import RecordItem from "@/custom";
import tagListModel from "@/models/tagListModel";

const tagList = tagListModel.fetch();
const recordList = recordListModel.fetch();

@Component({
  components: { Tags, FormItem, Types, NumberPad },
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

