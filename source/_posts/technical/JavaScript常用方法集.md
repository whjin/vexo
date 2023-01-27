---
title: JavaScript常用方法集
date: 2020-08-23 21:01:36
category: ["技术"]
tags: ["前端","JS"]
comments:
---

### 日期格式化

```JavaScript
// 格式化日期类型,fmt格式可选择
function dateFormat(fmt, date) {
  let ret;
  let opt = {
    "Y+": date.getFullYear().toString(), // 年
    "M+": (date.getMonth() + 1).toString(), // 月
    "D+": date.getDate().toString(), // 日
    "h+": date.getHours().toString(), // 时
    "m+": date.getMinutes().toString(), // 分
    "s+": date.getSeconds().toString(), // 秒
    "ms+": date.getMilliseconds().toString() // 毫秒
  };
  for (let k in opt) {
    ret = new RegExp("(" + k + ")").exec(fmt);
    if (ret) {
      fmt = fmt.replace(ret[1], ret[1].length == 1 ? opt[k] : opt[k].padStart(ret[1].length, "0"));
    }
  }
  return fmt;
}
let date = new Date();
let fDate = dateFormat("YYYY-MM-DD hh:mm:ss.ms", new Date(date));
```
<!--more-->

### 时间转换（秒数转时分秒）
```JavaScript
function timeFormat (sec) {
    let minite = Math.floor((sec / 60 % 60)) < 10 ? '0' + Math.floor((sec / 60 % 60)) : Math.floor((sec / 60 % 60));
    let second = Math.floor((sec % 60)) < 10 ? '0' + Math.floor((sec % 60)) : Math.floor((sec % 60));
    if (sec < 3600) {
        return `${minite}:${second}`;
    } else {
        let hour = Math.floor(sec / 3600) < 10 ? '0' + Math.floor(sec / 3600) : Math.floor(sec / 3600);
        return `${hour}:${minite}:${second}`;
    }
}
```

### 计算时分秒差值
```JavaScript
// 计算时分秒差值
function timeDiffer(beginTime, endTime) {
  let ret = {};
  let date = new Date();
  let sTime = Date.parse(dateFormat("YYYY/MM/DD", date) + " " + beginTime);
  if (beginTime >= endTime) {
    date.setDate(date.getDate() + 1);
  }
  let eTime = Date.parse(dateFormat("YYYY/MM/DD", date) + " " + endTime);
  let differ = eTime - sTime;
  let hour = Math.floor(differ / 1000 / 60 / 60);
  let minute = Math.floor(differ / 1000 / 60 - hour * 60);
  let second = Math.floor(differ / 1000 - hour * 60 * 60);
  ret = {
    differHour: hour,
    differMinute: minute,
    differSecond: second
  };
  return ret;
}
let { differHour, differMinute, differSecond } = timeDiffer(beginTime, endTime);
```
### 深拷贝
```JavaScript
// 深拷贝，即复制并独立一份数据，操作不影响原数据
function deepCopy(obj) {
  if (typeof obj !== "object") {
    return obj;
  }
  let result = Array.isArray(obj) ? [] : {};
  for (let i in obj) {
    if (obj.hasOwnProperty(i)) {
      if (typeof obj[i] === "object" && obj[i] !== null) {
        result[i] = deepCopy(obj[i]);
      } else {
        result[i] = obj[i];
      }
    }
  }
  return result;
}
```
### 数组去重
```JavaScript
// ES6最简方法
let result = [];
if (Array.isArray(arr)) {
  result = new Set(arr);
}

// 数组去重
function unique(arr) {
  if (!Array.isArray(arr)) {
    return;
  }
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    if (result.indexOf(arr[i]) === -1) {
      result.push(arr[i]);
    }
  }
  return result;
}
```
### 数组对象排序
```JavaScript
// 数组对象排序，比较两个字符串
list.sort((a, b) => {
  return a.id.localeCompare(b.id);
});
```

### 获取上/下个月日期
```JavaScript
// 下个月
let date = new Date(this.startDate);
let nextMonthDate = date.setMonth(date.getMonth() + 1);
this.endDate = dateFormat("YYYY-MM-DD", new Date(nextMonthDate));

// 上个月个月
let lastMonthDate = date.setMonth(date.getMonth() - 1);
```

### 获取前/后7天日期
```JavaScript
// 前7天
let date = new Date(this.startDate);
let afterDate = date.setDate(date.getDate() + 6);
this.endDate = dateFormat("YYYY-MM-DD", new Date(afterDate));

// 后7天
let afterDate = date.setDate(date.getDate() - 6);
```
