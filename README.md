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

1.  git cat-file -p HEAD

       -    Git이 실제로 무슨 일을 하는지 볼 때 유용하다.
___
2.   git ls-files -s
     -   명령은 훨씬 더 장막 뒤에 가려져 있는 명령으로 이를 실행하면 현재 Index가 어떤 상태인지를 확인할 수 있다   

3.   브런치 생성 및 변경
     
     a.   git branch {branchName}
        -       브랜치 만들
        
     b.   git checkout {branchName}
        -       현재 디렉토리 브랜치 변경
        -    git checkout -b {branchName}:생성과 체크아웃 동시에
        -    git checkout -b {newBranch} parentBranch:
                        
                        부모 branch 밑에 newBranch 생성   