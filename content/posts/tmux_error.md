---
title: "tmux を update したら起動しなくなった"
date: 2021-08-26T16:59:39+09:00
tags: [tmux]
showToc: false
TocOpen: false
draft: false
hidemeta: false
comments: false
description: ""
canonicalURL: ""
disableHLJS: false # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
---
何も考えずに `brew upgrade` で tmux のバージョンを上げたんだけど、起動しなくなってしまった。  
古い tmux server(session) が起動したままだったのが原因のよう。  
下記のように tmux server を殺すことで無事起動するようになった。  
たぶんすべての session を閉じることでもいけると思うんだけど、たくさん起動してたのでめんどくさくてやっちゃった。  

```shell
tmux kill-server
```

めでたしめでたし。
