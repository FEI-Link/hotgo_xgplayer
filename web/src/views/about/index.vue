<template>
  <div>
    <!-- 网络测试 -->
    <div class="n-layout-page-header">
      <n-card :bordered="false" title="关于">
        {{ name }} 是一个基于 goframe2，vue3，vite2，TypeScript，uniapp
        的中后台解决方案，它可以帮助你快速搭建企业级中后台项目，相信不管是从新技术使用还是其他方面，都能帮助到你，持续更新中。
      </n-card>
    </div>
    <n-card
      :bordered="false"
      title="项目信息"
      class="mt-4 proCard"
      size="small"
      :segmented="{ content: true }"
    >
      <n-descriptions bordered label-placement="left" class="py-2">
        <n-descriptions-item label="HotGo版本">
          <n-tag type="info"> {{ config?.version }}</n-tag>
        </n-descriptions-item>
        <n-descriptions-item label="最后编译时间">
          <n-tag type="info"> {{ lastBuildTime }} </n-tag>
        </n-descriptions-item>
        <n-descriptions-item label="文档地址">
          <div class="flex items-center">
            <a
              href="https://github.com/bufanyun/hotgo/tree/v2.0/docs/guide-zh-CN"
              class="py-2"
              target="_blank"
              >查看文档地址</a
            >
          </div>
        </n-descriptions-item>
        <n-descriptions-item label="预览地址">
          <div class="flex items-center">
            <a href="https://hotgo.facms.cn/admin" class="py-2" target="_blank">查看预览地址</a>
          </div>
        </n-descriptions-item>
        <n-descriptions-item label="Github">
          <div class="flex items-center">
            <a href="https://github.com/bufanyun/hotgo" class="py-2" target="_blank"
              >查看Github地址</a
            >
          </div>
        </n-descriptions-item>
        <n-descriptions-item label="QQ交流群">
          <div class="flex items-center">
            <a href="https://jq.qq.com/?_wv=1027&k=izJg29Cx" class="py-2" target="_blank"
              >点击链接加入群聊【HotGo 交流群】</a
            >
          </div>
        </n-descriptions-item>
      </n-descriptions>
    </n-card>

    <n-card
      :bordered="false"
      title="开发环境依赖"
      class="mt-4 proCard"
      size="small"
      :segmented="{ content: true }"
    >
      <n-descriptions bordered label-placement="left" class="py-2">
        <n-descriptions-item v-for="item in devSchema" :key="item.field" :label="item.field">
          {{ item.label }}
        </n-descriptions-item>
      </n-descriptions>
    </n-card>

    <n-card
      :bordered="false"
      title="生产环境依赖"
      class="mt-4 proCard"
      size="small"
      :segmented="{ content: true }"
    >
      <n-descriptions bordered label-placement="left" class="py-2">
        <n-descriptions-item v-for="item in schema" :key="item.field" :label="item.field">
          {{ item.label }}
        </n-descriptions-item>
      </n-descriptions>
    </n-card>
  </div>
</template>

<script lang="ts" setup>
  import { ref } from 'vue';
  import { useUserStoreWidthOut } from '@/store/modules/user';

  const useUserStore = useUserStoreWidthOut();
  const config = ref(useUserStore.config);
  export interface schemaItem {
    field: string;
    label: string;
  }

  const { pkg, lastBuildTime } = __APP_INFO__;
  const { dependencies, devDependencies, name } = pkg;

  const schema: schemaItem[] = [];
  const devSchema: schemaItem[] = [];

  Object.keys(dependencies).forEach((key) => {
    schema.push({ field: key, label: dependencies[key] });
  });

  Object.keys(devDependencies).forEach((key) => {
    devSchema.push({ field: key, label: devDependencies[key] });
  });
</script>

<style lang="less" scoped></style>
