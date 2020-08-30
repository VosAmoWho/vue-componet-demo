<template>
  <v-main>
    <div id="app" v-cloak>
      <tabs v-model="activeIndex">
        <pane label="科技" :closeable="true">
          科技
        </pane>
        <pane label="体育" :closeable="true">
          体育
        </pane>
        <pane label="娱乐" :closeable="true">
          娱乐
        </pane>
      </tabs>
    </div>
  </v-main>
</template>

<script>
import tabs from "@/components/Tabs"
import pane from "@/components/Pane"

export default {
  name: 'App',
  components: {
    tabs,
    pane
  },

  data: () => ({
    activeIndex: 0,
    close1: true,
  }),
};
</script>

<style>
[v-cloak] {
  display: none;
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
</style>
