# Vue 3 + Prism.js 程式碼高亮範例

這個專案展示了如何在 Vue 3 應用中使用 Prism.js 來實現程式碼高亮功能。

## 功能特點

- 使用 Vue 3 和 Vite 建立的專案
- 整合 Prism.js 實現程式碼高亮
- 支援行號顯示功能

## 前置需求

- Node.js (建議使用 node20.9.0 以上的 LTS 版本)
- pnpm (用於套件管理)

## 安裝 pnpm

如果您尚未安裝 pnpm，請執行以下命令進行安裝：

```bash
npm install -g pnpm
```

## 專案安裝

使用 pnpm 安裝依賴：

```bash
pnpm install
```

## 安裝 Prism.js

安裝 Prism.js 和相關的行號插件：

```bash
pnpm add prismjs
```

## 使用 Prism.js 進行程式碼高亮

在您的 Vue 組件中，可以這樣使用 Prism.js 來高亮程式碼：

```vue
<template>
  <pre v-pre class="language-javascript">
    <code ref="codeBlock">
      const message = 'Hello, World!';
      console.log(message);
    </code>
  </pre>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Prism from "prismjs";
import "prismjs/themes/prism.css";
import "prismjs/components/prism-javascript";

const codeBlock = ref(null);

onMounted(() => {
  Prism.highlightElement(codeBlock.value);
});
</script>

<style></style>
```

## 行號顯示

要在程式碼區塊中顯示行號，您可以使用 Prism.js 的行號插件。首先，在專案中引入行號插件的樣式和腳本：

```javascript
// main.js 或 main.ts
import 'prismjs/themes/prism.css';
import 'prismjs/plugins/line-numbers/prism-line-numbers.css';
import 'prismjs/plugins/line-numbers/prism-line-numbers.js';
```

然後，在您的 Vue 組件中，加入 `line-numbers` 類別來啟用行號顯示：

```vue
<template>
  <pre v-pre class="language-javascript line-numbers">
    <code ref="codeBlock">
      const message = 'Hello, World!';
      console.log(message);
    </code>
  </pre>
</template>
```

## 開發

啟動開發伺服器：

```bash
pnpm run dev
```

開啟瀏覽器並訪問 `http://localhost:5173`（端口號可能會有所不同），即可查看應用。

## 打包與預覽

要打包專案以進行生產部署，請執行：

```bash
pnpm run build
```

打包完成後，您可以使用預覽命令來本地查看打包結果：

```bash
pnpm run preview
```

## 文件結構

```
├── README.md
├── index.html
├── package.json
├── pnpm-lock.yaml
├── public
│   └── vite.svg
├── src
│   ├── App.vue
│   ├── assets
│   │   └── vue.svg
│   ├── components
│   │   ├── CodeBlock.vue
│   │   └── Example.vue
│   ├── main.js
│   └── style.css
└── vite.config.js
```

### 如何更改程式碼高亮的主題？

您可以在 `main.js` 中更改引入的 Prism.js 主題。例如，使用 `prism-okaidia` 主題：

```javascript
import 'prismjs/themes/prism-okaidia.css';
```

### 支援其他程式語言？

Prism.js 支援多種程式語言。只需在需要的地方引入相應的語言組件。例如，支援 Python：

```javascript
import 'prismjs/components/prism-python';
```

然後在程式碼區塊中使用 `language-python` 類別。

```vue
<div class="line-numbers">
		<pre><code class="language-python">
    你的程式碼
    </code></pre>
</div>
```

##### 其他參考資料

- [Prism.js 官方文件](https://prismjs.com/docs/)
- [Add Prism.js to a Vue Application](https://dev.to/kevin_odongo35/add-prism-js-to-a-vue-application-3e9p)
- [Vue 3 中使用 Prism.js 實現程式碼高亮](https://www.tuziki.com/coder/article/659bc57747d522c7ba4d49f1)
- [vite-plugin-prismjs](https://www.npmjs.com/package/vite-plugin-prismjs)
- [使用 Prismjs 让你写的代码高亮起来（以 Vue3 为例）](https://blog.csdn.net/qq_43030820/article/details/131918105)