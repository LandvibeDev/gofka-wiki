# Git

- 목차
  1. Git의 구조
  2. ssh key 등록
  3. 브랜치따서 PR 올리기



## 1. Git의 구조

![](assets/2019-06-17-21-33-14.png)

### 1.1 Working Directory(내컴퓨터)
- 작업을 하고 있는 공간
- `.git` 파일이 생성된 디렉토리의 하위 디렉토리들
- git이 디렉토리들의 파일 변화를 감지한다.


### 1.2 Stage Area(스테이지 영역)
- git에서 관리하고 싶은 파일들을 Stage 영역로 옮긴다
- Stage 영역에 포함되지 않은 파일들은 Repository로 커밋되지 않는다.
- `git add ${파일명}` 명령어로 특정 파일을 스테이지 영역으로 옮길 수 있다.

### 1.3 Local Repository(로컬 저장소)
- Stage 영역에서 관리하는 파일들의 변경사항이 저장되는 곳
- `git commit` 명령어로 변경사항을 로컬 저장소에 추가할 수 있다.
- 많이 쓰는 옵션
  - `git commit -a`: 변경되거나 삭제된 파일을 자동적으로 스테이지 영역에서 제외시킨다.(주의! 새로운 파일을 추가하지는 않음.)
  - `git commit -m ${메세지}`: 커밋 메세지를 같이 추가한다.


### 1.4 Remote Repository(원격 저장소)
- 내 컴퓨터가 아닌 git 서버(Github, Gitlab, Bitbucket)
- 근본적으로 로컬 저장소와 같다.
- 로컬에 저장하는 것은 유실의 위험이 있으니 Github과 같은 안전한 클라우드 서버에 소스를 보관하기 위한 목적을 가지고 있다.
- 원격 저장소에 소스를 저장하면 소스의 공유, 코드 리뷰 등의 협업이 가능해진다.
- `git push ${remote 저장소 이름} ${remote 저장소 branch}`
- 사용 예시
  - `git push origin master`
  - `git push upstream master`
  - `git push origin feature/add-readme`


## 2. ssh key 등록



## 3. branch따서 PR 올리기