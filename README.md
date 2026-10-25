# ps5-build-deps

`quark-ps5`（PS5 夸克网盘客户端）构建过程中需要的、**原始地址在 CI 环境不可达**的依赖镜像。

## 内容

| Release | 资产 | 原始地址 | 不可达原因 | sha256 |
|---|---|---|---|---|
| `unrar-7.2.1` | `unrarsrc-7.2.1.tar.gz` | www.rarlab.com/rar/unrarsrc-7.2.1.tar.gz | rarlab 屏蔽数据中心 IP（GitHub runner Errno 101） | `3fe3b4d710da45521625353dc2e023dad48c010f02a93302756e1061a8f3ae8e` |

所有资产均为官方发布的逐字节镜像，消费方（ps5-react 的 dependencies.lock.json）
以 sha256 强校验，内容不符会直接构建失败，不存在静默错包风险。

## 为什么需要公开

GitHub Actions 对**私有**仓库的 release 资产也要鉴权，而 ps5-react 的 `fetch()`
不带凭据；公开资产无需鉴权，CI 与本地构建行为一致，无需为构建改框架代码。
