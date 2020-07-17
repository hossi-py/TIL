# Git

> Git은 분산형 버전 관리 시스템, Distributied Version Control System (DVCS)이다.
>
> 소스코드의 버전 및 이력을 관리할 수 있다.



## 준비하기

윈도우에서 Git을 활용하기 위해서 Git Bash를 설치한다.

Git을 활용하기 위해서 Graphic User Interface (GUI) Tool인 `Source Tree` , `Github Desktop` 등을 활용할 수도 있다.

초기 설치를 완료한 이후에 컴퓨터에 Author 정보를 입력한다.

```bash
$ git config --global user.name  {user name}
$ git config --global user.email {user email}
```



## 로컬 저장소(Repository) 활용하기

### 1. 저장소 초기화

```bash
$ git init
Initialized empty Git repository in C:/users/hossi/temp/.git/
```

* `.git` 폴더가 생성되며, 여기에 Git과 관련된 모든 정보가 저장된다.
* Git Bash에 (master) 라고 표시 되는데, 이는 현재 폴더가 Git으로 관리되고 있다는 뜻이며, `master` branch에 있다는 뜻이다.



### 2. `add`

`working directory`, 즉, 작업 공간에서 변경된 사항을 이력으로 저장하기 위해서는 반드시 `staging area`를 거쳐야 한다.

```bash
$ git add {파일or폴더}
$ git add markdown.md	# 파일
$ git add images/		# 폴더
$ git add .				# 현재 디렉토리(.)에 있는 모든 파일과 폴더
```



- `add` 전 상태 (markdown.md 파일이 폴더에 새롭게 작성되었으나, 아직 Git으로 관리되지 않은 상태)

```bash
$ git status
On branch master

No commits yet

untracked files:
  (use "git add <file>..." to include in what will be committed)
        new file:   markdown.md
        
    
nothing added to commit but untracked files present (use "git add" to track)
```



- `add` 후 상태 (markdown.md 파일이 `add` 후, staging area로 올라간 상태)

```bash
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   markdown.md
```



### 3. `commit`

`commit`은 **이력을 확정짓는 명령어**로, 해당 시점의 Snapshot을 기록한다.

`commit`을 할 때, 반드시 메시지를 작성해야하며, **메시지는 변경사항을 알 수 있도록 명확하게 작성한다.**

```bash
$ git commit -m "마크다운 정리"
[master (root-commit) 8ebbe6a] 마크다운 정리
 1 file changed, 170 insertions(+)
 create mode 100644 markdown.md
```

`commit`이후에는 아래의 명령어를 통해 지금까지 작성된 `commit`이력을 확인한다.

```bash
$ git log
commit 8ebbe6add7e15c7f82787345142f5acfc74bcb3d (HEAD -> master) # commit의 hash 값 (중복되지 않음)
Author: hossi-py <hossi0128@gmail.com>
Date:   Fri Jul 17 11:48:48 2020 +0900

	마크다운 정리
	
$ git log --oneline												# 여러 개의 commit을 한 줄에 보기
8ebbe6a (HEAD -> master, origin/master) 마크다운 정리
```



## 원격 저장소(Remote Repository) 활용하기

원격 저장소 기능을 제공하는 다양한 서비스 중에 Github를 기준으로 설명한다.



### 0. 준비사항

- Github에 Repository 생성하기



### 1. 원격 저장소 등록

```bash
$ git remote add origin {github url}
```

- 원격저장소(`remote`)로 origin이라는 이름으로 github url을 등록(`add`)한다.
- 등록된 원격저장소를 보기 위해서는 아래의 명령어를 활용한다.

```bash
$ git remote -v
origin  https://github.com/hossi-py/TIL.git (fetch)
origin  https://github.com/hossi-py/TIL.git (push)
```



### 2. `push` 

> `push` = 원격 저장소로 업로드

```bash
$ git push origin master
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 2.02 KiB | 2.02 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/hossi-py/TIL.git
 * [new branch]      master -> master
```

`origin` 이라는 이름의 원격 저장소로 `commit` 기록들을 업로드한다.

이후 변경사항이 생길 때마다, `add` - `commit` - `push` 를 반복한다.