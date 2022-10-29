---
title: Web SQL浏览器数据库实例
date: 2020-08-23 20:55:31
category: ["前端"]
tags: ["前端"]
comments:
---

> 最近在做一个消息定时器，需要在离线环境中使用，通过表单写入事项存储到本地，渲染在表格中。尝试过使用Node.js进行文件读写操作，受到UI框架的限制；同时测试了localStorage存储，也达不到想要的效果。最后直接使用WebSql和indexDB来完成。以下是一个DEMO，实际效果正在测试中...

<!--more-->

```html
// html
<button id="btn-create">创建user数据表</button>
<button id="btn-insert">插入数据</button>
<button id="btn-query">查询数据</button>
<button id="btn-update">修改数据</button>
<button id="btn-delete">删除数据</button>
<button id="btn-drop">删除user数据表</button>
<div id="websql"></div>
<script src="server.js"></script>
```
```JavaScript
// JavaScript
let findId = (id) => document.getElementById(id);

let db = openDatabase("MySql", "1.0", "Test DB", 2 * 1024 * 1024);
let result = db ? "数据库创建成功" : "数据库创建失败";
let websql = document.getElementById("websql");
websql.innerHTML = result;

// 创建数据表
const USER_TABLE_SQL =
  "create table if not exists userTable (username varchar(12)," + "password varchar(16),info text)";
function createTable() {
  db.transaction((tx) => {
    tx.executeSql(
      USER_TABLE_SQL,
      [],
      (tx, result) => {
        websql.innerHTML = "创建user表成功" + result;
      },
      (tx, error) => {
        websql.innerHTML = "创建user表失败" + error.message;
      }
    );
  });
}

// 插入数据
const INSERT_USER_SQL = "insert into userTable (username,password,info) values (?,?,?)";
function insertData(user) {
  db.transaction((tx) => {
    tx.executeSql(
      INSERT_USER_SQL,
      [user.username, user.password, user.info],
      (tx, result) => {
        websql.innerHTML = "添加数据成功" + result;
      },
      (tx, error) => {
        websql.innerHTML = "添加数据失败" + error.message;
      }
    );
  });
}

// 查询数据
const QUERY_USER_SQL = "select * from userTable";
function queryData() {
  db.transaction((tx) => {
    tx.executeSql(
      QUERY_USER_SQL,
      [],
      (tx, result) => {
        websql.innerHTML = "查询数据成功" + JSON.stringify(result.rows);
      },
      (tx, error) => {
        websql.innerHTML = "查询数据失败" + error.message;
      }
    );
  });
}

// 修改数据
const UPDATE_USER_SQL = "update userTable set username=?,password=?,info=? where rowid=1";
function updateData(user) {
  db.transaction((tx) => {
    tx.executeSql(
      UPDATE_USER_SQL,
      [user.username, user.password, user.info],
      (tx, result) => {
        websql.innerHTML = "修改数据成功";
      },
      (tx, error) => {
        websql.innerHTML = "修改数据失败" + error.message;
      }
    );
  });
}

// 删除数据
const DELETE_USER_SQL = "delete from userTable where rowid=(select Max(rowid) from userTable)";
function deleteData(user) {
  db.transaction((tx) => {
    tx.executeSql(
      DELETE_USER_SQL,
      [],
      (tx, result) => {
        websql.innerHTML = "删除数据成功";
      },
      (tx, error) => {
        websql.innerHTML = "删除数据失败" + error.message;
      }
    );
  });
}

// 删除数据表
const DROP_USER_SQL = "drop table userTable";
function dropTable() {
  db.transaction((tx) => {
    tx.executeSql(
      DROP_USER_SQL,
      [],
      (tx, result) => {
        websql.innerHTML = "删除数据表成功";
      },
      (tx, error) => {
        websql.innerHTML = "删除数据表失败" + error.message;
      }
    );
  });
}

let user = {
  username: "李宇春",
  password: "abc123456",
  info: "快乐女声->中国好声音",
};
let btnCreate = findId("btn-create");
let btnInsert = findId("btn-insert");
let btnQuery = findId("btn-query");
let btnUpdate = findId("btn-update");
let btnDelete = findId("btn-delete");
let btnDrop = findId("btn-drop");
btnCreate.onclick = () => createTable();
btnInsert.onclick = () => insertData(user);
btnQuery.onclick = () => queryData();
btnUpdate.onclick = () => updateData(user);
btnDelete.onclick = () => deleteData(user);
btnDrop.onclick = () => dropTable();
```
