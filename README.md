# LearningGit
-   MacBook Git  터미널 자동완성  설정

        1.brew install git bash-completion

        2.vi ~/.bash_profile  

     3.내용 복붙 

    >[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion

        4.source ~/.bash_profile 



-   용어 정리
    1.  HEAD:
   
            HEAD는 현재 브랜치를 가리키는 포인터이며, 브랜치는 브랜치에 담긴 커밋 중 가장 마지막 커밋을 가리킨다. 지금의 HEAD가 가리키는 커밋은 바로 다음 커밋의 부모가 된다. 단순하게 생각하면 HEAD는 현재 브랜치 마지막 커밋의 스냅샷 이다.
    2.  Index
                    
                Index는 바로 다음에 커밋할 것들이다. 이미 앞에서 우리는 이런 개념을 Staging Area'' 라고 배운 바 있다. Staging Area'' 는 사용자가 git commit 명령을 실행했을 때 Git이 처리할 것들이 있는 곳이다.
                먼저 Index는 워킹 디렉토리에서 마지막으로 Checkout 한 브랜치의 파일 목록과 파일 내용으로 채워진다. 이후 파일 변경작업을 하고 변경한 내용으로 Index를 업데이트 할 수 있다. 이렇게 업데이트 하고 git commit 명령을 실행하면 Index는 새 커밋으로 변환된다.

-   git Command 설명

## 1.  git cat-file -p HEAD

       -    Git이 실제로 무슨 일을 하는지 볼 때 유용하다.
___
## 2.   git ls-files -s
     -   명령은 훨씬 더 장막 뒤에 가려져 있는 명령으로 이를 실행하면 현재 Index가 어떤 상태인지를 확인할 수 있다   
---
## 3.   브런치 생성 및 변경
     
a.   git branch {branchName}
        -       브랜치 만듬
        
b.   git checkout {branchName}
-    현재 디렉토리 브랜치 변경
-    git checkout -b {branchName}:생성과 체크아웃 동시에
-    git checkout -b {newBranch} parentBranch:
- 부모 branch 밑에 newBranch 생성
---
## 4. [종류](https://gmlwjd9405.github.io/2018/05/11/types-of-git-branch.html)

> 메인 브랜치들(master, develop)과 일정 기간 동안만 유지되는 보조 브랜치들(feature, release, hotfix)
        
 ###     1. master
        
-   제품으로 출시될 수 있는 브랜치
        배포(Release) 이력을 관리하기 위해 사용. 즉, 배포 가능한 상태만을 관리한다.
###      2. develop
- 기능 개발을 위한 브랜치들을 병합하기 위해 사용. 즉, 모든 기능이 추가되고 버그가 수정되어 배포 가능한 안정적인 상태라면 develop 브랜치를 ‘master’ 브랜치에 병합(merge)한다.평소에는 이 브랜치를 기반으로 개발을 진행한다.
      
###      3. Feature
-    feature 브랜치는 새로운 기능 개발 및 버그 수정이 필요할 때마다 **‘develop’** 브랜치로부터 분기한다. feature 브랜치에서의 작업은 기본적으로 공유할 필요가 없기 때문에, 자신의 로컬 저장소에서 관리한다.
      -    예) feature/login(기능명)
###      4. Release
- 이번 출시 버전을 준비하는 브랜치
배포를 위한 전용 브랜치를 사용함으로써 한 팀이 해당 배포를 준비하는 동안 다른 팀은 다음 배포를 위한 기능 개발을 계속할 수 있다. 즉, 딱딱 끊어지는 개발 단계를 정의하기에 아주 좋다.
예를 들어, ‘이번 주에 버전 1.3 배포를 목표로 한다!’라고 팀 구성원들과 쉽게 소통하고 합의할 수 있다는 말이다.

-  예) release-1.2(버전)
###      5. HotFix
- 포한 버전에 긴급하게 수정을 해야 할 필요가 있을 경우, ‘master’ 브랜치에서 분기하는 브랜치이다. ‘develop’ 브랜치에서 문제가 되는 부분을 수정하여 배포 가능한 버전을 만들기에는 시간도 많이 소요되고 안정성을 보장하기도 어려우므로 바로 배포가 가능한 ‘master’ 브랜치에서 직접 브랜치를 만들어 필요한 부분만을 수정한 후 다시 ‘master’브랜치에 병합하여 이를 배포해야 하는 것이다.
- 예) hotfix-1.2.1  




---
## 5. git push origin (branch)[default:master]
     - 해당 branch를 origin(repo)에 저장에 등록하고 push한다
---
## 6. Merge

## git merge [--no-ff] branch1
### (현재 checkout되있는 branch에 branch1을 병합)
### a. ff(Fast-Forward)

     - 병합 시 현재 check out되 있는 branch(master)를 합칠 branch(feature)를 가르키게 함
     - 새로운 commit 객체 생성 x, y자가 아닌(즉 후진 하지 않고 도달할 수 있을 때) 경우  깃은 그냥 merge시 ff로 동작
     - 트리가 한 줄이라 깔끔하다


###   b. --no-ff

     - 브랜치가 갈라져서 기능적으로 구분 할 수 있다.
     - master와 feature 모두 담은 새로운 commit 객체를 만든다
     - 보통 Y자에서 쓰임 
     - 이후 현재 checkout되 있는 branch를 해당 새로운 commit으로 옮김
     
###   c. conflict
     - Y자 구조에서 같은 파일의 내용을 다르게 변경하여 충돌하는 상황
     - FF에서는 발생하지 않음 (Y자가 아니라)
     - 이 때 둘중하나를 고르게함 
     - 이 것을 사전 방지하기 위한 기능이 rebase이다.
---
## 7. Rebase
### git rebase [branch] 
  - 해당 branch를 현재 checkout branch로 base를 옮긴다.
### a.  옮겨진 branch는 checkout branch의 기능 까지 모두 포함
     
 - 예 master:UI:1.4 feature:UI:1.0,payment 기능 있음(Y자)
 - git rebase feature 하면 feature가 master뒤로 가며 ,UI:1.4, payment기능이 있다.
 - 이후 git merge feature를 하면 FF가 되어 master가 feature를 가르킨다.
 - 만약에 feature에서 UI를 건드려 master와 conflict가 발생 시 rebase 할 때 conflict를 미리 알려주기 때문에 거기서 수정하게 된다.
---
## 8. reset

### git reset [--옵션] 돌아갈 위치(commit id or HEAD ~인덱스번호)
## 해당 위치로 상태를 돌린다.
## 옵션 종류(해당 상태 전으로)
###  (--hard)[working directory 까지 모두 날림]
>a.txt의 내용 수정: a->b
### (--mixed) :add 전으로 되돌린다(unstaging)
>git add .
### (--soft) : commit 전으로 되돌린다
>git commit

### 9. tag
[관련 페이지](https://webisfree.com/2017-07-31/git-%ED%83%9C%EA%B9%85%ED%95%98%EA%B8%B0-tag-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
## git tag


     
