[![Build Status](https://travis-ci.org/wusthuke/traviscidemo.svg?branch=master)](https://travis-ci.org/wusthuke/traviscidemo)


## commit -> push -> commit -> push -> merge -> commit -> accept

| sha                                      | suite_id | status    | conclusion      | appId | appName    | head sha                                 |
|:-----------------------------------------|:---------|:----------|:----------------|:------|:-----------|:-----------------------------------------|
| 38462d959a40a6eed03671e39577d270150e9948 | 10651917 | queued    | null            | 67    | Travis CI  | 38462d959a40a6eed03671e39577d270150e9948 |
|                                          | 10651918 | completed | action_required | 11006 | App Center |                                          |
| faca4cdda5259be19dcbe719a9d7b0a2daa48cbf | 10651256 | queued    | null            | 67    | Travis CI  | faca4cdda5259be19dcbe719a9d7b0a2daa48cbf |
|                                          | 10651257 | completed | action_required | 11006 | App Center |                                          |

head sha: 38462d959a40a6eed03671e39577d270150e9948

before: faca4cdda5259be19dcbe719a9d7b0a2daa48cbf

## commit -> commit -> push -> commit -> push -> merge -> accept

| sha                                      | suite_id | status    | conclusion      | appId | appName    | head_sha                                 |
|:-----------------------------------------|:---------|:----------|:----------------|:------|:-----------|:-----------------------------------------|
| 0f5c7fbd520468e5c3ec7dd618b2ac186acbab3e |          |           |                 |       |            |                                          |
| b1e6dd701cd563ee1ea4d71be68082c70e523752 | 10660305 | queued    | null            | 67    | Travis CI  | b1e6dd701cd563ee1ea4d71be68082c70e523752 |
|                                          | 10660306 | queued    | null            | 11006 | App Center | 同上                                      |
| fc3f4b2b17a009560ac1e1d8e8232eb1a77e1c8d | 10660356 | queued    | null            | 67    | Travis CI  | fc3f4b2b17a009560ac1e1d8e8232eb1a77e1c8d |
|                                          | 10660357 | completed | action_required | 11006 | App Center | 同上                                      |

**结论：** push 时，创建 check_suite web hook,
但是只有pull_request发生变更(创建 or 新的push加入)时，check run
才会被真正创建.


## commit -> push -> merge -> commit -> push -> rerun -> accept

| op            | sha                                      | suite_id | status    | conclusion      | appId | appName    | check_run_size | run_id   | run_name                 |
|:--------------|:-----------------------------------------|:---------|:----------|:----------------|:------|:-----------|:---------------|:---------|:-------------------------|
| commit + push | 47e8693b2e477e08b3572bb8983abcbc2c8912d5 | 12897458 | queued    | null            | 67    | Travis CI  | 0              | 无       |                          |
| -             | -                                        | 12897459 | queued    | null            | 11006 | App Center | 0              | 无       |                          |
|               |                                          |          |           |                 |       |            |                |          |                          |
| merge         | 47e8693b2e477e08b3572bb8983abcbc2c8912d5 | 12897458 | queued    | null            | 67    | Travis CI  | 0              | 无       |                          |
|               |                                          | 12897459 | completed | action_required | 11006 | App Center | 1              | 无       | traviscidemo for Android |
|               |                                          |          |           |                 |       |            |                |          |                          |
| commit + push | a67ce313a7af0c25a7e1d9be1cdee362393cb903 | 12899226 | queued    | null            | 67    | Travis CI  | 0              | 无       |                          |
|               |                                          | 12899227 | completed | action_required | 11006 | App Center | 1              | 16177509 | 同上                      |
|               |                                          |          |           |                 |       |            |                |          |                          |
| rerun         | a67ce313a7af0c25a7e1d9be1cdee362393cb903 | 12899226 | queued    | null            | 67    | Travis CI  | 0              | 无       |                          |
|               |                                          | 12899227 | completed | action_required | 11006 | App Center | 1              | 16177509 | 同上                      |


### service级别通知示例

namespace(kedou.hk)一级添加了service定义，service的范围为 public

> 1. namespace级别管理员添加了service, 使用.
> 2. kedou.hk -> test 发生变更，check_suite_webhook


service若有资源在使用，则不能被删除。service要排除部分应用

1. 获取service是否有在被使用。
2. 获取使用某service的场景。

a b
=======
a

b ad a ad aaa a
