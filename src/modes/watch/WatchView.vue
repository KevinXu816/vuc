<template>
  <VucCollapsePanel title="watch" extra-icon="md-add" @extra-click="editData">

    <vuc-code-list :data="VucWatchs" @click-item="editData" @delete-item="delData"></vuc-code-list>

    <Modal title="编辑" v-model="editState" width="800" @on-ok="saveData" :mask-closable="false">
      <WatchForm :vucAst="vucAst" :data="curData"></WatchForm>
    </Modal>

  </VucCollapsePanel>
</template>

<script>

  import designerMixins from '../designerMixins.js';
  import WatchForm from './WatchForm.vue';

  export default {
    components: {
      WatchForm,
    },

    mixins: [designerMixins],

    data () {
      return {
        curData: null,
        editState: false,
      };
    },

    computed: {
      VucWatchs () {
        if (this.vucAst) {
          return this.vucAst.VucWatchs;
        }
        return [];
      },
    },

    methods: {
      editData (data) {
        this.curData = Object.assign(
          {
            id: undefined,
            name: undefined,
            value: undefined,
          }, data);

        this.editState = true;
      },

      saveData () {
        this.vucAst.saveWatch(this.curData);
      },

      delData (data) {
        this.vucAst.delWatch(data);
      },

    },
  };

</script>
