## GitHub

**Commit**

: 변경사항과 버전을 남기는 것



**Staging area**: 

변경사항 저장 전 임시저장

안전장치를 만드는 것

### 초기 setting

### $ git config --global user.name 유저이름

### $ git config --global user.email 이메일

### $ git config --global -l

참고사항: 1이 아닌 alphabet L이다.

설정을 확인하는 것이다.

### $ git inti

깃을 시작한다는 의미이다.

**참고사항**

- ~ : Home directory에서는 git init를 하지 않는다.
- 이미 git이 관리하고 있는데 다시 git을 실행하지 않는다.

### $ git add 파일이름

파일을 staging area에 올려둔다는 의미이다.

파일이 git에 의해 관리되기 시작한다.

### $ git add .

해당 폴더의 모든 파일들을 staging area에 추가하는 것을 의미한다.

### $ git status

git이 관리하고 있는 파일들의 상태를 확인하는 방법이다.

예)

On branch master

No commits yet

nothing to commit (create/copy files and us "git add" to track)



On branch master

No commits yet

Untracked files:

(use "git add \<file>..." to include in what will be committed)

​		a.txt

nothing added to commit but untracked files present (use "git add" to track)



On branch master

No commits yet

Changes to be committed:

(use "git rm --cached \<file>..." to unstage)



### $ git commit -m '메세지'

'메세지'라는 변경사항을 담아서 commit을 남기는 것

### $ git log

commit 상태를 확인하는 것

### $ git log --oneline

commit 상태를 확인하는 git log를 oneline으로 확인할 수 있도록 하는 것

### $ git long -숫자

commit 상태를 숫자의 갯수만큼만 확인하는 것



## GitHub와 연결

### $ git init

### GitHub Repository 만들기

GitHub 주소 복사하기

### $ git remote add origin url

git으로 원격으로 연결할 것이다. origin이라는 별명을 붙일 것이다.

= GitHub의 주소를 \'origin'이라는 별명으로 원격 연결할 것이다.

### $ git remote -v

원격으로 어디에 연결되어 있는 지 확인 하는 것

### $ git push origin master

\'origin이라는 별명을 가진 GitHub Repository의 master branch에 push할 것이다.

### $ git push -u orignin master

origin master는 계속 사용하니 설정을 저장하여 이후에는 생략할 것이다.

이후에는 git push만 입력해도 push가 가능하다.

### $ git commit

git commit 을 입력하게 되면 **VIM text editor**가 나오게 된다.

i를 입력하면 insert모드가 되어 입력이 가능하다.

shift + enter를 두번 누르면 색이 다르게 작성 가능하다.

내용은 git log --oneline이 아닌 git log에서 볼 수 있다.

ESC를 눌러 insert모드에서 나올 수 있다.

:wq를 입력하여 저장 후 나올 수 있다.

### $ git remote rm 별명

$ git remote -v를 했을때 동일한 주소가 다른 이름으로 저장되었을 경우와 같을 때 사용한다.

Remote 제거 코드이다.

### $ rm *.txt

.txt의 확장자를 가진 모든 파일을 지우는 것

### $ rm-rf .git

git 위치를 다시 설정하고 싶은 경우에 사용한다.

기존에 git init를 했던 directory에서 입력하면 .git 이 삭제된다.

## Clone

### $ git clone url

git이 아닌 상태에서 GitHub의 Repository를 복사해서 오는 것

가장 처음 1번하면 된다.

1. git clone url : Repository의 이름으로 폴더를 생성하여 clone
2. git clone url . : Git Bash가 실행된 폴더에 clone
3. git clone url 폴더이름 : 폴더이름을 생성하여 clone

3가지 방법이 있고 1번째 방법을 사용해봤다.

### $ git pull

최초의 clone 이후 (또는 이미 Git인 상태에서 ) GitHub의 commit으로 최신화 시키는 것

### git clone 폴더에서는 git init는 수행하지 않아도 된다.

$ git pull ($ touch a.txt) $ git add . $ git commit -m '메세지' $ git push 를 반복하는 작업을 통해 최신의 것을 GitHub에 Push한다.

### $ git log 결과를 통해 Push 결과확인

Push를 통해 업데이트가 잘 되었는지 확인하는 방법

결과가 (HEAD -> master, origin/master, origin/HEAD)가 한 줄에 나타날 경우 업데이트가 잘 되었다는 의미이다.

만약 (HEAD -> master)와 (origin/master, origin/HEAD)가 다른 줄에 나타날 경우 Push가 필요하다는 의미이다.

## Branch

### $ git branch

어떤 branch가 존재하는지, *이 있는 것이 현재 branch

### $ git branch 브랜치 이름

branch를 만든다.

### $ git switch 브랜치 이름

해당 브랜치로 옮긴다.

### $ git branch -c 브랜치이름

브랜치를 만들고 동시에 해당 브랜치로 옮긴다.

### $ git branch -d 브랜치이름

브랜치를 삭제한다.

### $ git merge 브랜치이름

현재 branch에서 브랜치이름을 병합시킨다.

### $ git checkout master



### $ git reset --hard (commit id)

commit id는 git log를 통해 확인할 수 있다.

#### CONFLICT (pull에서도 마찬가지)

A'B + AB' = A'B'

A' + A'' = CONFLICT!

* CONFLICT에서 해결 후 add, commit
