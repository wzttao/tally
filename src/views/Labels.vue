<template>
  <Layout>
    <div class="createTag-wrapper">
      <Button class="createTag"
              @click="createTag">新建标签
      </Button>
    </div>
    <div class="tags">
      <router-link class="tag" v-for="tag in tags" :key="tag.id"
                   :to="`/labels/edit/${tag.id}`">
        <span>{{ tag.name }}</span>
        <Icon name="right"/>
      </router-link>
    </div>
  </Layout>
</template>

<script lang="ts">
import {Component} from 'vue-property-decorator';
import Button from '@/components/Button.vue';
import {mixins} from 'vue-class-component';
import TagHelper from '@/mixins/TagHelper';

@Component({
  components: {Button},
})
export default class Labels extends mixins(TagHelper) {
  get tags() {
    return this.$store.state.tagList;
  }

  beforeCreate() {
    this.$store.commit('fetchTags');
  }
}
</script>

<style lang="scss" scoped>
.createTag {
  height: 40px;
  color: #ffffff;
  background: #767676;
  border: none;
  border-radius: 5px;
  padding: 0 14px;

  &-wrapper {
    text-align: center;
    padding: 5px;
    margin-bottom: 5px;
  }
}

.tags {
  background: #ffffff;
  font-size: 16px;
  padding-left: 16px;
  margin-top: 16px;

  .tag {
    min-height: 44px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid #e6e6e6;

    svg {
      margin-right: 16px;
    }
  }
}

.createTag {

}

</style>