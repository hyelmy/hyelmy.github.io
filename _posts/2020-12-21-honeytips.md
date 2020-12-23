---
title: "github 블로그 운영할 때  꿀팁"
excerpt: "커밋 하기전 미리보기방법, vim 단축키 등등!"

categories:
  - "끄적끄적"
tags:
  - "끄적끄적"
  - "꿀팁"
last_modified_at: 2020-12-21
---

## 1. 커밋하기 전 미리보는 방법

이 방법을 알기 전, 항상 커밋,  푸시를 하고 블로그가 어떻게 변경되었는지 확인했어야했다.

```
bundle exec jekyll serve
```
위 코드를 사용해서 터미널에서 로컬 서버를 띄우면 미리보기가 가능하다.







## 2. vim 단축키 정리

나는 코드를 짤 때 vim으로 자주 다루는데, vim을 쓸 때 단축키를 알아두면 정말 편하다!
그래서 정리해본 자주 쓰는 단축키들!

j,k,h,l 상,하,좌,우

w,b 단어단위 좌,우

shift+{} 문단단위

v 선택, V 줄선택

<,> 들여쓰기

x 글자 삭제

r 수정 

shift+r insert 모드

y 복사 

p 붙여넣기

d 삭제

H,L,M 맨위, 맨아래, 정중앙

ctrl+u,d 반페이지씩 위,아래이동

u 취소

ctrl+R 취소하기전으로



[얄팍한 코딩사전 유튜브 주소](://www.youtube.com/watch?v=qn1soztN7k4&t=303s) 이 영상을 참고해보면 vim을 왜 쓰면 좋은지 잘 설명되어있다. 친구 추천으로 보게 된 유튜버인데 설명을 쉽게 해줘서 유용한 것 같다!







## 3. github 블로그 운영하는데 도움을 많이 받은 블로그

처음 github 블로그를 만들 때 정말 많은 도움을 받은 블로그이다.
참고하면 좋음! 이 분처럼 도움을 줄 수 있는 블로그를 잘 만들어보고싶다!

<https://devinlife.com/>







## 4. git 푸시할 때마다 로그인 하지 않는 방법

git을 사용하다보면 푸시 할 때마다 github 아이디와 비밀번호를 입력하라고 뜬다.
이러한 과정이 귀찮을 시, 이 방법을 사용해보자.

```
ls ~/.ssh
```
위 명령어를 입력해서 id_rsa.pub, id_rsa 파일이 있는지 확인을 하자!

없을 경우, 
```
ssh-keygen
```
위 명령어를 입력해서 SSH키인 id_rsa.pub, id_rsa 파일을 생성하자.

(id_rsa는 private key, id_rsa.pub은 public key라서, id_rsa가 있으면 id_rsa.pub을 다른 곳에 등록해서 사용할 수 있다고 한다. 두 개의 파일은 열쇠-자물쇠같은 단짝이라고 볼 수 있다.)


```
ls ~/.ssh
```
두 파일이 잘 생겼는지 확인해보자.
SSH키가 잘 생성이 되었으면 

```
cat ~/.ssh/id_rsa.pub
```
출력된 SSH키를 복사를 하여 

Github page->Settings->SSH keys-> SSH키 붙여넣고 등록해주면 된다!



그리고 꼭 필요한 과정!!!!!(중요! 안하면 등록한 SSH키를 사용할 수 없음)

Github 사이트에서 자동로그인 시킬 레파지토리로 들어가 Code->Clone에서 SSH주소를 복사한다.
터미널에서 해당 git 저장소로 들어가 해당 명령어를 입력해준다.
```
git config remote.origin.url 복사한 SSH주소
git config remote.origin.url git@github.com:~~~~~~~~.git
```

이 과정이 끝나고 푸시를 해보면 github 아이디, 비밀번호를 입력하지 않아도 푸시를 할 수 있게 된다!
