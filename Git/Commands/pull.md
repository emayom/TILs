---
title: git pull
category: Git
tags:
  - Git
  - Commands
date: 2024-02-20T00:00:00.000Z
last_modified_at: '2024-12-13T06:15:18.860Z'
---

# git pull 

git pull 명령어는 원격 저장소의 변경 사항을 작업 중인 로컬 브랜치로 가져와서 병합하는 편리하고 필수적인 명령어입니다.  
그러나 git pull 명령어가 하나의 작업 단위가 아닌 페칭(i.e., git fetch)과 병합(i.e., git merge)를 수행하는 두 명령어의 조합이라는 것을 종종 간과합니다.

## git pull의 동작 방식 
```
git pull [<options>] [<repository> [<refspec>…​]]
```
git pull 명령어의 동작 방식은 아래와 같습니다. 

1. 주어진 파라미터들로 원격 저장소의 변경 사항을 다운로드하기 위해 `git fetch`를 실행한다. 
2. config 옵션, 명령줄의 플래그에 따라 `git rebase` 또는 `git merge`를 실행하여 분기된 브랜치들을 조정한다.  

    > pull.rebase=false이거나 `--rebase`, `--no-rebase` 플래그가 없다면 기본적으로 merge를 수행한다. 

결국 git fetch와 git merge로 분리하여 실행해도 git pull을 실행한 것과 동일한 결과를 얻을 수 있지만,  
대부분의 사용자가 개별적으로 실행하는 것보다 간편하게 한 번에 처리할 수 있다는 점에서 git pull을 선호할 것입니다. 

하지만 반대로 변경 사항을 병합하는 과정에서 **'일부 제어권이 개발자의 손에서 떠나가는게 아닌가?'** 하는 의문이 들었습니다. 

개발자가 명시적으로 fetch와 merge/rebase를 실행하여 변경 사항을 확인하고 병합할 때와는 달리, git pull은 자동으로 이러한 과정을 수행하므로 예상치 못한 결과가 발생할 수 있습니다. 

#### 명시적인 단계를 
- 변경 사항을 병합 이전에 확인할 수 있다. 
- 예상치 못한 결과를 방지하고, 상황과 목적에 따라 적절한 병합 전략을 선택할 수 있다.  
- 작업 흐름을 더욱 명확하게 이해하고 관리할 수 있다. 

### `--rebase` 옵션 - 불필요한 병합 커밋 방지 
개발자들이 rebase를 선호하는 경우를 흔하게 볼 수 있다.  
선형적인 히스토리 유지하기 

## 마치며 
단순 사용을 넘어, 다양한 명령어를 효과적으로 활용하기 위해서는 각 명령어가 수행하는 용도와 동작 방식을 정확히 이해하는 것 또한 중요하다는 것을 새삼 느낄 수 있었습니다.    

원격 저장소에서 브랜치의 변경 사항을 검토할 필요가 없다면 git pull은 효율적인 선택지일 수 있지만, 
불편하더라도 git pull 이전에 git fetch를 통해 origin의 변경 사항을 확인한 후 팀의 선호 방식이나 규칙에 따라 병합을 수행하는 습관을 기르는 것이 더욱 안전하고 효과적일 수 있다.

> #### References  