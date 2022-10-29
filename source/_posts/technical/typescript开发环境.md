---
title: typescript开发环境
date: 2019-10-13 21:43:15
category: ["前端","typescript"]
tags: ["typescript"]
comments: true
---

**安装编译工具**

```javascript
"scripts": {
  "start": "tsc && concurrently \"npm run tsc:w\" \"npm run lite\"",
  "lite": "lite-server",
  "tsc": "tsc",
  "tsc:w": "tsc -w"
},
"devDependencies": {
  "concurrently": "^5.0.0",
  "lite-server": "^2.5.4"
}
```

<!--more-->
