<template>
  <div class="tabs">
    <div class="tabs-bar">
      <div
          :class="tabClass(item)"
          v-for="(item,index) in titleList"
          :key="index"
          @click="change(index)"
      >
        {{ item.label }}
        <span v-if="item.closeable" class="close" @click="close(index,item.name)"></span>
      </div>
    </div>
    <div class="tabs-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "tabs",
  props: {
    value: {
      type: [String, Number]
    }
  },
  data: function () {
    return {
      currentIndex: this.value,
      titleList: [],
    }
  },
  methods: {
    tabClass: function (item) {
      return ['tabs-tab', {
        'tabs-tab-active': (item.name === this.currentIndex)
      }]
    },
    getTabs() {
      return this.$children.filter((item) => {
        return item.$options.name === 'pane'
      })
    },
    updateIsShowStatus() {
      let tabs = this.getTabs()
      let that = this
      tabs.forEach((tab, index) => {
        return tab.isShow = (index === that.currentIndex)
      })
    },
    change: function (index) {
      let nav = this.titleList[index]
      let name = nav.name
      this.$emit('input', name)
    },
    init() {
      this.titleList = []
      let that = this
      this.getTabs().forEach((tab, index) => {
        that.titleList.push({
          label: tab.label,
          closeable: tab.closeable,
          name: index
        })
        if (index === 0) {
          if (!that.currentIndex) {
            that.currentIndex = index
          }
        }
      })
      this.updateIsShowStatus()
    },
    close: function (index, name) {
      this.titleList.splice(index, 1);
      let tabs = this.getTabs();
      tabs.forEach(function (tab, index) {
        if (index === name) {
          return tab.isShow = false;
        }
      });
    }
  },
  watch: {
    value: function (val) {
      this.currentIndex = val
    },
    currentIndex: function () {
      this.updateIsShowStatus()
    }
  }
}
</script>

<style scoped>
.tabs {
  font-size: 14px;
  color: #657180;
}

.tabs-bar:after {
  content: '';
  display: block;
  width: 100%;
  height: 1px;
  background: #d7dde4;
  margin-top: -1px;
}

.tabs-tab {
  display: inline-block;
  padding: 4px 16px;
  margin-right: 6px;
  background: #fff;
  border: 1px solid #d7dde4;
  cursor: pointer;
  position: relative;
}

.tabs-tab:hover {
  color: #336699;
  font-weight: bolder;
}

.tabs-tab-active {
  color: #336699;
  border-top: 1px solid #336699;
  border-bottom: 1px solid #fff;
}

.tabs-tab-active:before {
  content: '';
  display: block;
  height: 1px;
  background: #3399ff;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
}

.tabs-content {
  padding: 8px 0;
}

.close {
  color: #FF6666;
}

.close::before {
  content: "\2716";
}

.close:hover {
  color: #990033;
  font-weight: bolder;
}

.tabs-tab-active {
  color: #336699;
  border-top: 1px solid #336699;
  border-bottom: 1px solid #fff;
  transform:translateY(-1px);
  transition: transform 0.5s;
}

</style>