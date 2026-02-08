<template>
  <div class="set" @mouseenter="closeShow = true" @mouseleave="closeShow = false" @click.stop>
    <transition name="el-fade-in-linear">
      <close-one
        class="close"
        theme="filled"
        size="28"
        fill="#ffffff60"
        v-show="closeShow"
        @click="store.setOpenState = false"
      />
    </transition>
    <el-row :gutter="40">
      <el-col :span="12" class="left">
        <div class="logo text-hidden">
          <span class="bg">{{ siteUrl[0] }}</span>
          <span class="sm">.{{ siteUrl[1] }}</span>
        </div>
        <div class="version">
          <div class="num">v&nbsp;{{ config.version }}</div>
          <el-tooltip content="Github 源代码仓库" placement="right" :show-arrow="false">
            <github-one class="github" theme="outline" size="24" @click="jumpTo(config.github)" />
          </el-tooltip>
        </div>
        <div class="image-wrap">
          <img src="https://api.imlazy.ink/img" alt="decoration" />
        </div>
      </el-col>
      <el-col :span="12" class="right">
        <div class="title">
          <setting-two theme="filled" size="28" fill="#ffffff60" />
          <span class="name">全局设置</span>
        </div>
        <Set />
      </el-col>
    </el-row>
  </div>
</template>

<script setup>
import { CloseOne, SettingTwo, GithubOne } from "@icon-park/vue-next";
import { mainStore } from "@/store";
import Set from "@/components/Set.vue";
import config from "@/../package.json";

const store = mainStore();
const closeShow = ref(false);

const siteUrl = computed(() => {
  const url = import.meta.env.VITE_SITE_URL;
  if (!url) return "zient.top".split(".");
  if (url.startsWith("http://") || url.startsWith("https://")) {
    const urlFormat = url.replace(/^(https?:\/\/)/, "");
    return urlFormat.split(".");
  }
  return url.split(".");
});

const jumpTo = (url) => {
  window.open(url);
};
</script>
<style lang="scss" scoped>
.set {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80%;
  height: 80%;
  background: rgb(255 255 255 / 40%);
  border-radius: 6px;
  padding: 40px;

  .close {
    position: absolute;
    top: 14px;
    right: 14px;
    width: 28px;
    height: 28px;
    cursor: pointer;

    &:hover {
      transform: scale(1.2);
    }

    &:active {
      transform: scale(1);
    }
  }

  .el-row {
    height: 100%;
    flex-wrap: nowrap;

    .left {
      height: 100%;
      padding-left: 40px !important;
      padding-bottom: 20px;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      gap: 24px;

      .logo {
        font-family: "Pacifico-Regular";
        padding-left: 22px;
        width: 100%;
        height: auto;
        min-height: auto;
        transform: none;
        
        .bg {
          font-size: 3.5rem;
        }

        .sm {
          margin-left: 6px;
          font-size: 1.5rem;
        }

        @media (max-width: 990px) {
          .bg { font-size: 3rem; }
          .sm { font-size: 1.3rem; }
        }
        @media (max-width: 825px) {
          .bg { font-size: 2.5rem; }
          .sm { font-size: 1.1rem; }
        }
      }

      .version {
        display: flex;
        flex-direction: row;
        align-items: center;

        .num {
          font-size: 1.5rem;
          font-family: "Pacifico-Regular";
        }

        .github {
          width: 22px;
          height: 22px;
          margin-left: 10px;
          margin-top: 4px;
          cursor: pointer;

          &:hover {
            transform: scale(1.2);
          }
        }
      }

      .image-wrap {
        flex: 1;
        width: 100%;
        min-height: 150px;
        border-radius: 8px;
        overflow: hidden;
        background: rgba(255, 255, 255, 0.2);
        
        img {
          width: 100%;
          height: 100%;
          object-fit: cover;
          display: block;
        }
      }
    }

    .right {
      height: 100%;
      padding-right: 40px !important;
      display: flex;
      flex-direction: column;
      justify-content: flex-start; // 从 center 改为 flex-start，顶部对齐
      padding-top: 20px; // 可选：加一点顶部间距

      .title {
        display: flex;
        align-items: center;
        flex-direction: row;
        font-size: 18px;
        margin-bottom: 16px;

        .i-icon {
          width: 28px;
          height: 28px;
          margin-right: 6px;
        }
      }
    }
  }
}
</style>