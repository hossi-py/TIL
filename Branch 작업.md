# Branch 작업 [A104]

[TOC]

## 0. Branch 구조

- master - develop
- develop에서 소스코드 관리를 합니다.

### 1) Branch 이름 설정 (기능 만들 때)

```bash
$ git branch 이니셜_기능

# 예시)
$ git branch HYH_mainPage
$ git branch OMT_login
```



### 2) Commit 규칙

```bash
[frontend]
$ git commit -m "[front] 로고 작업 "

[backend_spring]
$ git commit -m "[back_s] 로그인 기능 구현"

[backend_python]
$ git commit -m "[back_p] 회원가입 기능 구현"
```



## 1. Maintainer일 때

- 프로젝트 생성 후 develop 브런치를 만들어줍니다.

```bash
$ git branch develop
```

- develop 브런치로 이동합니다.

```bash
$ git switch develop
$ git checkout develop 도 가능하니 둘 중에서 편한거 쓰시면 됩니다.
```

- 기능 구현을 위한 branch를 만듭니다.

``` bash
$ git branch HYH_mainPage
```

- HYH_mainPage branch로 이동합니다.

```bash
$ git switch HYH_mainPage
```

- `코드 작성 -> 마무리` 가 되었다면, 아래 처럼 입력합니다.

```bash
$ git add .
$ git commit -m "[Front] 메인페이지 UI 구현"
$ git push origin HYH_mainPage

### 주의 ###
# push를 할 때 origin master가 아닌 orgin 기능 구현 중인 브런치로 해주어야 합니다.
```

- `push`가 되었으면, `Maintainer` 는 깃랩에서 `merge`를 할 수 있습니다.
- `프로젝트 메인 메뉴` - `프로젝트 이름 하단`에 있는 `branches`를 눌러줍니다.
- 본인 혹은 팀원들의 `merge request` / `Compare`를 볼 수 있습니다.
- `Compare`를 누르면 변동 사항을 확인할 수 있습니다.
- `Merge request`를 누르고 `Description`에 설명을 적습니다.
- 하단에 초록색 버튼 `Submit merge request`를 누르기 전에 바로 위에 있는
- `Source branch` 는 기능 구현 한 브런치(HYH_mainPage),  `Target branch`는 develop으로 설정합니다.
- 이후, `Submit merge request`를 누르고 `Merge`를 누릅니다.
- bash로 돌아와서, 아래와 같이 코드를 작성해줍니다.

```bash
$ git switch develop
$ git pull origin develop
```

- 수정된 코드가 develop에 적용된 것을 확인 할 수 있습니다.
- 기능 구현이 끝난 branch는 삭제해줍니다.

```bash
$ git branch -d HYH_mainPage
```

- 같은 방식으로 develop branch에서 소스코드를 관리해주면 됩니다.



## 2. Developer일 때

- 먼저 develop branch에서 완성 후 이상이 없으면 master에 올리도록 하겠습니다.

1. 각자 작업할 branch를 만들어서 작업합니다.
2. 완성이 되면 push합니다.

```bash
git add .
git commit -m "~~"
git push origin (branch 이름)
```

3. develop branch로 이동합니다.

```bash
$ git checkout develop			// switch 쓰셔도 됩니다.
...(develop)					// 헤더 위치가 develop
```

4. 작업한 branch를 merge합니다.

```bash
$ git merge (branch 이름)
```

5. **merge 된 branch는 꼭 지워 주셔야 됩니다.**

```bash
$ git branch -d (branch 이름)
```

6. develop도 완성되면 push해서 master랑 merge 요청하시면 됩니다.



#### 지켜야 할 것

1. commit 양식은 통일한 것으로 지켜주세요.
2. branch 이름은 기능 구현에 대해 정해야 관리하기 편하다고 합니다.
3. 다른 사람이 작업 중인 파일은 작업이 끝난 후 수정해주세요. 아니면 한쪽 작업을 다 날려야됩니다.
4. master로 push하셔도 올라가지 않으니 branch만 push해주세요.



## 3. 작업이 겹칠 때 [서로 다른 기능 branch에서 작업]

### 1) 다른 사람이 Push 했을 때

- 나의 기능 branch에서 `add / commit / push` 를 한다.
- 먼저 `push`한 사람이 `merge`를 하거나 관리자가 한다.
- 나의 기능 branch에서 `pull develop`을 한다.

```bash
$ git switch develop
$ git merge "나의 기능 branch"
$ git push origin develop
```

을 하면 된다.



### 2) 다른 사람이 Merge 했을 때

- 나의 기능 branch에서 `add / commit` 을 한다.
  - `push`는 오류가 생긴다.
- 나의 기능 branch에서 `pull develop`을 한다.

```bash
$ git switch develop
$ git merge "나의 기능 branch"
$ git push origin develop
```

을 하면 된다.



