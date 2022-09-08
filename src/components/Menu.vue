<template>
  <div style="width: 200px">
    <a-button type="primary" style="margin-bottom: 16px" @click="toggleCollapsed">
      <MenuUnfoldOutlined v-if="collapsed" />
      <MenuFoldOutlined v-else />
    </a-button>
    <a-menu v-model:openKeys="openKeys" v-model:selectedKeys="selectedKeys" mode="inline" theme="dark"
      :inline-collapsed="collapsed">
      <a-menu-item key="1" @click="setVisable">
        <template #icon>
          <UploadOutlined />
        </template>
        <span>上传模型</span>
      </a-menu-item>
      <a-menu-item key="2">
        <template #icon>
          <DesktopOutlined />
        </template>
        <span>Option 2</span>
      </a-menu-item>
      <a-menu-item key="3">
        <template #icon>
          <InboxOutlined />
        </template>
        <span>Option 3</span>
      </a-menu-item>
      <a-sub-menu key="sub1">
        <template #icon>
          <MailOutlined />
        </template>
        <template #title>Navigation One</template>
        <a-menu-item key="5">Option 5</a-menu-item>
        <a-menu-item key="6">Option 6</a-menu-item>
        <a-menu-item key="7">Option 7</a-menu-item>
        <a-menu-item key="8">Option 8</a-menu-item>
      </a-sub-menu>
      <a-sub-menu key="sub2">
        <template #icon>
          <AppstoreOutlined />
        </template>
        <template #title>Navigation Two</template>
        <a-menu-item key="9">Option 9</a-menu-item>
        <a-menu-item key="10">Option 10</a-menu-item>
        <a-sub-menu key="sub3" title="Submenu">
          <a-menu-item key="11">Option 11</a-menu-item>
          <a-menu-item key="12">Option 12</a-menu-item>
        </a-sub-menu>
      </a-sub-menu>
    </a-menu>
  </div>
  <div class="ULButton">
    <UpLoadButton :getVisable="visable" />
  </div>
</template>
<script lang="ts">
import { defineComponent, reactive, toRefs, watch,ref } from 'vue';
import {
  MenuFoldOutlined,
  MenuUnfoldOutlined,
  PieChartOutlined,
  MailOutlined,
  DesktopOutlined,
  InboxOutlined,
  AppstoreOutlined,
  UploadOutlined,
} from '@ant-design/icons-vue';
import UpLoadButton from './UpLoadButton.vue';
export default defineComponent({
  components: {
    MenuFoldOutlined,
    MenuUnfoldOutlined,
    PieChartOutlined,
    MailOutlined,
    DesktopOutlined,
    InboxOutlined,
    AppstoreOutlined,
    UploadOutlined,
    UpLoadButton,
  },
  setup() {
    const state = reactive({
      collapsed: false,
      selectedKeys: ['1'],
      openKeys: ['sub1'],
      preOpenKeys: ['sub1'],
    });
    const visable=ref(false)
    watch(
      () => state.openKeys,
      (_val, oldVal) => {
        state.preOpenKeys = oldVal;
      },
    );
    const toggleCollapsed = () => {
      state.collapsed = !state.collapsed;
      state.openKeys = state.collapsed ? [] : state.preOpenKeys;
    };
    const setVisable = () => {
      visable.value = !visable.value;
    };
    return {
      ...toRefs(state),
      toggleCollapsed,
      visable,
      setVisable
    };
  },
});
</script>

<style>
div {
  overflow: hidden;
  position: fixed;
}

.ULButton {
  left: 12%;
  top: 8%;
}
</style>
  
  