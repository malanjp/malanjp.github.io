---
title: "Prisma2 + Promise.all() とかやるとコネクション数制限に引っかかってエラーになる件"
date: 2021-07-28T15:10:01+09:00
draft: false
toc: false
images:
tags: 
  - untagged
  - Prisma2
  - RDB
  - PostgreSQL
---

RDB に Prisma2 を用いてクエリを投げるのはよくやると思うんですが、`Promise.all()` とかして物凄い勢いで非同期実行するとこんなエラーが出がち。  
あと `connection_limit` を引き上げろって言われてるけど、GCP のコンソールでグラフを見ている限り、実際には同時クエリ実行数で怒られてるように見える。  

> Timed out fetching a new connection from the pool. Please consider reducing the number of requests or increasing the `connection_limit` parameter (https://www.prisma.io/docs/concepts/components/prisma-client/connection-management#connection-pool). Current limit: 100.

.env の `DATABASE_URL` に `pool_timeout=0` を指定してやるとずっと待ってくれるので回避できる。  
とはいえ 0 だと永久に待つらしいので、普通は 30sec 程度で殺すようにしたほうがいいと思う。  
あと connection_limit, socketTimeout, connectTimeout の調整も必要であればやる。  

```env
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/hoge?schema=public&connection_limit=100&pool_timeout=0&socketTimeout=0&connectTimeout=0
```
