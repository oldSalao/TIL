- git 명령어

  - git

    git의 명령어들을 볼 수 있다.

  - git init

    현재 디렉토리에서 git 작업을 시작한다. 저장소의 뼈대를 담고있는 .git 디렉터리가 생성되며 이 디렉터리에는 추후 버전관리를 할 때 생성되는 정보들이 저장된다.

  - git clone \<url\>

    원격 저장소를 clone 한다. clone시 자동으로 origin이라는 단축이름이 생성된다.

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

  - git checkout -- <파일>

    수정한 파일을 최근 커밋된 버전으로 복구한다.(수정한 내용이 사라지기 때문에 주의.)

  - git remote [-v]

    현재 프로젝트에 등록된 리모트 저장소를 확인할 수 있다. 리모트 저장소의 단축 이름을 보여준다. -v 옵션으로 단축이름과 URL을 함께 볼 수 있음.

  - git remote add <단축이름> \<url\>

    워킹 디렉토리에 리모트 저장소 추가.

  - git fetch <리모트 저장소 이름>

    리모트 저장소에서 데이터를 가져온다. 로컬에는 없지만 리모트 저장소에는 있는 데이터를 모두 가져온다. merge는 수동으로 해줘야 함.

  - git pull <리모트 이름> <리모트브랜치 이름>

    리모트 저장소에서 데이터를 가져올 뿐만 아니라 자동으로 로컬 브랜치와 merge 시킬 수 있다.

  - git push <리모트 이름><리모트브랜치 이름>

    리모트 저장소에 push한다. 저장소를 clone한 다른 사람이 push를 하면 merge를 먼저 한 후에 push할 수 있다.

  - git remote show <리모트 저장소 이름>

    리모트 저장소의 구체적인 정보 확인. git pull 명령을 실행할 때 master 브랜치와 merge할 브랜치가 무엇인지 보여준다.

  - git remote rename <원래이름> <바꿀이름>

    리모트 저장소의 이름을 변경한다.

  - git remote remove

    리모트 저장소 삭제.

  - git branch

    브랜치의 목록을 보여준다.

  - git branch <브랜치이름>

    새로운 브랜치를 생성한다.

  - git branch -d <브랜치이름>

    브랜치를 삭제한다. 병합되지 않은 브랜치를 강제로 삭제하려면 -D 사용.

  - git checkout <브랜치이름>

    HEAD가 가리키는 브랜치를 변경한다.

  - git log --oneline --decorate --graph --all

    브랜치가 가리키고 있는 히스토리와 어떻게 갈라져 나왔는지를 보여준다.

  - git merge <브랜치이름>

    입력한 브랜치와 현재 브랜치를 merge한다.

  - git branch --merged <브랜치이름>

    병합된 브랜치들의 목록을 보여준다.(브랜치 이름 미지정시 현재 브랜치 기준.)

  - git branch --no-merged <브랜치이름>

    병합되지않은 브랜치들의 목록을 보여준다.(브랜치 이름 미지정시 현재 브랜치 기준.)

  - git remote show <리모트 이름>

    모든 리모트 브랜치와 그 정보를 보여줌.

  - git checkout -b <로컬 브랜치> <리모트>/<리모트 브랜치>

    로컬브랜치를 생성하고 생성된 브랜치가 리모트브랜치를 트래킹하도록 한다.

  - git branch -u <리모트>/<리모트 브랜치>

    이미 로컬에 존재하는 브랜치가 리모트의 특정 브랜치를 트래킹하게 한다.

  - git branch -vv

    추적 브랜치가 어떻게 설정되어 있는지 확인한다.

  - git push <리모트> --delete <리모트 브랜치>

    리모트 브랜치를 삭제한다.

  - [참고](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-%EB%B2%84%EC%A0%84-%EA%B4%80%EB%A6%AC%EB%9E%80%3F)
