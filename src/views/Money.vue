<template>
  <Layout class-prefix="layout">
    <!--    {{ record }}-->
    <numberPad :value.sync="record.amount" @submit="saveRecord"/>
    <Tabs :data-source="recordTypeList" :value.sync="record.type"/>
    <div class="InputItem-wrapper">
      <InputItem field-name="备注"
                 placeholder="在这里输入备注"
                 :value.sync="record.notes"/>
    </div>
    <Tags @update:value="record.tags = $event"/>
  </Layout>
</template>

<script lang="ts">
import NumberPad from '@/components/Money/NumberPad.vue';
import InputItem from '@/components/Money/InputItem.vue';
import Tags from '@/components/Money/Tags.vue';
import Vue from 'vue';
import {Component} from 'vue-property-decorator';
import Tabs from '@/components/Tabs.vue';
import recordTypeList from '@/constants/recordTypeList';

@Component({
  components: {Tabs, Tags, InputItem, NumberPad},
})
export default class Money extends Vue {
  record: RecordItem = {tags: [], notes: '', type: '-', amount: 0};
  recordTypeList = recordTypeList;

  get recordList() {
    return this.$store.state.recordList;
  }

  created() {
    this.$store.commit('fetchRecords');
  }

  // onUpdateNotes(value: string) {
  //   this.record.notes = value;
  // }

  saveRecord() {
    if (!this.record.tags || this.record.tags.length === 0) {
      return window.alert('请选择至少一个标签');
    }
    this.$store.commit('createRecord', this.record);
    if(this.$store.state.createRecordError === null){
      window.alert('已保存')
    }
    this.record.notes = '';
  }
}
</script>

<style lang="scss">
.layout-content {
  display: flex;
  flex-direction: column-reverse;
}

.InputItem-wrapper {
  padding: 10px 0;
}
</style>