<template>
  <div class="van-tab__pane" :class="{ 'van-tab__pane--select': index === parentGroup.curActive }">
    <slot></slot>
  </div>
</template>

<script>
import { create } from '../utils';
import findParent from '../mixins/find-parent';

export default create({
  name: 'van-tab',

  mixins: [findParent],

  props: {
    title: {
      type: String,
      required: true
    },
    disabled: Boolean
  },

  computed: {
    index() {
      return this.parentGroup.tabs.indexOf(this);
    }
  },

  created() {
    this.findParentByName('van-tabs');
    this.parentGroup.tabs.push(this);
  },

  destroyed() {
    this.parentGroup.tabs.splice(this.index, 1);
  }
});
</script>
