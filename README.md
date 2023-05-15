# 您好，歡迎來到 Wayne Lu 的輪播 project

這個輪播功能使用 html + css + JavaScript + Vue 製作而成

概念是在 ul 做 v-for="(img, index) in imgs"將 5 個 li 標籤引入圖片 imgs

用一個 div 將這個 ul 列表包起來

在這個 div 加上 position: relative

讓這 5 張圖片重疊在同一位置

宣告一個 showCarousel = ref(0) 的 ref 值

藉由操控這個 ref 值來達到輪播的效果

# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).
