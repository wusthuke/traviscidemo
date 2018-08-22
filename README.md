[![Build Status](https://travis-ci.org/wusthuke/traviscidemo.svg?branch=master)](https://travis-ci.org/wusthuke/traviscidemo)

## test

## go

## commit -> merge -> commit -> accept

| sha                                      | suite_id | status    | conclusion      | appId | appName    |
|:-----------------------------------------|:---------|:----------|:----------------|:------|:-----------|
| 38462d959a40a6eed03671e39577d270150e9948 | 10651917 | queued    | null            | 67    | Travis CI  |
|                                          | 10651918 | completed | action_required | 11006 | App Center |
| faca4cdda5259be19dcbe719a9d7b0a2daa48cbf | 10651256 | queued    | null            | 67    | Travis CI  |
|                                          | 10651257 | completed | action_required | 11006 | App Center |

head sha: 38462d959a40a6eed03671e39577d270150e9948

before: faca4cdda5259be19dcbe719a9d7b0a2daa48cbf

after: 38462d959a40a6eed03671e39577d270150e9948

pull_request: https://api.github.com/repos/wusthuke/traviscidemo/pulls/4

当提交的sha为branch_name时，默认选择当前branch下的最后一次commit_id.  每次提交，只要加入到了pull_request，都会新穿件 check_suite

## commit -> commit -> merge -> accept
