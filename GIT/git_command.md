- git 명령어

  - git

    git의 명령어들을 볼 수 있다.

  - git init

    현재 디렉토리에서 git 작업을 시작한다. 저장소의 뼈대를 담고있는 .git 디렉터리가 생성되며 이 디렉터리에는 추후 버전관리를 할 때 생성되는 정보들이 저장된다.

  - git clone \<url\>

    원격 저장소를 clone 한다.

  - git status

    저장소에 있는 파일들의 상태를 확인한다. Untracked(관리대상이 아님.), Tracked(관리대상임.)

  - git add

    파일을 추적하고 관리하도록 한다. (Untracked => Tracked) 파일을 Staged 상태로 만든다. 파일,디렉터리를 add할 수 있다 \*을 사용하면 모든 파일 add.

  - git commit -m "커밋메시지"

    커밋 메시지와 함께 staged 상태의 파일들에 대한 커밋 수행.

  - git log [-p]

    저장소의 커밋 히스토리를 확인할 수 있다. -p 옵션은 각 커밋의 diff까지 확인할 수 있게 해준다. 그 외 옵션은 [참고](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%BB%A4%EB%B0%8B-%ED%9E%88%EC%8A%A4%ED%86%A0%EB%A6%AC-%EC%A1%B0%ED%9A%8C%ED%95%98%EA%B8%B0)

  - git diff [--staged]

    staging area의 파일(staged된 파일)과 워킹디렉토리의 파일(staged 되지 않은 파일)간의 차이를 확인할 수 있다. --staged 옵션 적용시 commit된 파일과 staging area의 파일간의 차이 확인.

  - git rm [--cached]

    staging area와 워킹 디렉토리에서 파일을 삭제. --cached 옵션으로 Staging area 에서만 삭제할수도 있다.

  - git mv <기존 파일명> <변경할 파일명>

    파일의 이름을 변경한다.

  - git commit --amend

    커밋을 재작성할 수 있다.

  - git reset HEAD <파일>

    staging area의 파일을 unstaged 상태로 변경한다.

  - git checkout -- <file>

    수정한 파일을 최근 커밋된 버전으로 복구한다.(수정한 내용이 사라지기 때문에 주의.)

  - git remote [-v]

    현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다. 리모트 저장소의 단축 이름을 보여준다. -v 옵션으로 단축이름과 URL을 함께 볼 수 있음.

  - git remote add <단축이름> \<url\>

    워킹 디렉토리에 리모트 저장소 추가.

  - git fetch <리모트 저장소 이름>

    리모트 저장소에서 데이터를 가져온다.

  - [참고](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%EB%9E%80%3F)
