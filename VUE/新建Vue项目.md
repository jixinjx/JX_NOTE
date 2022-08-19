## 新建Vue项目
```
npm install -g @vue/cli
```

安装 @vue/cli-int：
```
npm i -g @vue/cli-init
```

## 安装element-plus

```
# NPM
$ npm install element-plus --save

```

### 完整引入[#](https://element-plus.gitee.io/zh-CN/guide/quickstart.html#完整引入)

如果你对打包后的文件大小不是很在乎，那么使用完整导入会更方便。

```
// main.ts
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)

app.use(ElementPlus)
app.mount('#app')
```
