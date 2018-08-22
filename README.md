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

after: 38462d959a40a6eed03671e39577d270150e9948

pull_request: https://api.github.com/repos/wusthuke/traviscidemo/pulls/4

当提交的sha为branch_name时，默认选择当前branch下的最后一次commit_id.
每次提交，只要加入到了pull_request，都会新穿件 check_suite

## commit -> commit -> push -> commit -> push -> merge -> accept

| sha                                      | suite_id | status    | conclusion      | appId | appName    | head_sha                                 |
|:-----------------------------------------|:---------|:----------|:----------------|:------|:-----------|:-----------------------------------------|
| 0f5c7fbd520468e5c3ec7dd618b2ac186acbab3e |          |           |                 |       |            |                                          |
| b1e6dd701cd563ee1ea4d71be68082c70e523752 | 10660305 | queued    | null            | 67    | Travis CI  | b1e6dd701cd563ee1ea4d71be68082c70e523752 |
|                                          | 10660306 | queued    | null            | 11006 | App Center | 同上                                      |
| fc3f4b2b17a009560ac1e1d8e8232eb1a77e1c8d | 10660356 | queued    | null            | 67    | Travis CI  | fc3f4b2b17a009560ac1e1d8e8232eb1a77e1c8d |
|                                          | 10660357 | completed | action_required | 11006 | App Center | 同上                                      |

**结论：** push 时，创建 check_suite web hook, 但是只有pull_request发生变更(创建 or 新的push加入)时，check run 才会被真正创建.