<template>
  <div>
    <div class="cell-border" style="background:#f8f8f9;font-size:14px;color:#515A6E">
      <Strong>Checker scripts</Strong>
    </div>
    <CellGroup v-if="checkerList.length" @on-click="onClickCell" class="checker-list">
      <Cell 
        class="cell-border" 
        v-for="checker in checkerList" 
        title="With Switch" 
        :key="checker.name"
        :name="checker.name"
        :selected="checker.select"
      >
        <Tooltip content="Debug" placement="bottom-start" :delay="500" transfer>
          <Icon v-if="checker.debug" type="ios-build" color="#2b85e4" size="16"/>
        </Tooltip>
        {{checker.name}}
        <i-switch slot="extra" v-model="checker.activated" size="small" @on-change="changeStatus(checker)"></i-switch>
      </Cell>
    </CellGroup>
    <div v-else class="checker-empty">
      No scripts
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    checkerList() {
      return this.$store.state.checker.checkers
    }
  },
  methods: {
    onClickCell(name) {
      this.$store.commit('setFocusChecker', name)
      this.$store.dispatch('loadCheckerDetail', name)
    },
    changeStatus(checker) {
      this.$store.dispatch('updateCheckerStatus', checker)
    }
  }
}
</script>

<style>
.checker-list {
  height: calc(100vh - 99px);
  /* total:100vh
    header: 38px
    textBar: 32px
    border: 1px
    list
    footer: 28px
  */
  overflow-y: auto;
  margin-right: 0;
}
.cell-border {
  padding: 5px 5px;
  border-bottom: 1px dashed #dcdee2;
}
.ivu-cell-group > .ivu-cell {
  padding: 5px 5px;
  border-bottom: 1px dashed #dcdee2;
}
</style>
