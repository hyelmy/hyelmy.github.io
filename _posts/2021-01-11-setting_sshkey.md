---
title: "Github ssh key 생성, 등록하는 방법"
excerpt: "ssh key를 생성해서 Github에 등록해서 사용해보자~!"
classes: wide
categories:
  - "끄적끄적"
tags:
  - "끄적끄적"
  - "꿀팁"
last_modified_at: 2020-01-11
---

github 블로그 운영할 때 꿀팁에 써놨지만 좀 더 자세한 과정이 필요할 것 같아 정리해본다!


ssh key를 생성하는 이유는 Github 접속 할 때 마다 번거롭게 로그인을 계속 해야되는 과정을 생략할 수 있기 때문이다!


# 1. SSH 키 생성하기

## 1. SSH키를 생성하기 전 먼저 SSH키가 있는지 확인한다

```ls ~/.ssh```

파일이나 디렉토리가 없다하면 2번 과정으로 넘어간다.
만약 id_rsa id_rsa.pub 파일이 있다면 이미 만든 ssh키가 있기 떄문에 새로 만들 필요는 없다!

## 2. SSH키를 생성한다 


```ssh-keygen -t rsa -b 4096 -C "email@example.com"```

옵션
  - -t: 생성할 키 타입
  - -b: 생성할 키의 비트 수
  - -C: 코멘트. 대문자에 주의!!

email@example.com은 Github에 등록되어있는 이메일을 작성하면 된다!

Enter 이름, 비밀번호를 생성하라고 뜨는데 엔터를 치고 넘어갈 수 있다.

키 파일의 이름이나, 비밀번호를 더 생성해서 보안성을 높이고 싶으면 해도된다.

이후에 The key fingerprint is:라고 뜨면 ssh키가 생성 완료 된 것 이다!


## 3. ssh키가 잘 생성 되었는지 확인해보자

```ls ~/.ssh``` 

id_rsa, id_rsa.pub 파일이 있다면 잘 생성 완료 된 것이다

id_rsa는 private key, id_rsa.pub키는 public key이므로 id_rsa.pub을 다른 곳에 등록해서 사용할 수 있다

이 2개의 파일은 열쇠-자물쇠같은 단짝이라고 볼 수 있다.

# 2. Github ssh key 사용하기

## 1. 다음으로 에이전트에 ssh key를 동록한다.

```eval `ssh-agent -s` ```

eval 명령어
- eval 은 인수로 주어지는 스트링을 한번 evaluation 한 후에 결과를 다시 명령문으로 실행한다.


ssh-agent 쓰는 이유
  - ssh-agent 쓰지 않고도 ssh키 가지고 아이디, 비밀번호 없이 원격 서버에 접속 할 수 있지만, 만약 ssh key를 생성할 때 비밀 번호를 생성했을 시, 개인키의 비밀번호를 암호화 해 기억해두고 처음 한번만 개인키 비밀번호를 입력하면 다음부터는 기억한 비밀번호를 이용하므로 사용자는 또 비밀 번호를 입력하지 않아도 된다고 한다.


## 2. 그리고 private key(id_rsa)를 agent에 추가한다. 

```ssh-add ~/.ssh/id_rsa```



# 3. ssh키 Github에 등록하기

## 1. id_rsa.pub키의 내용을 cat으로 읽어 복사한다.

```cat ~/.ssh/id_rsa.pub```

위 명령어를 사용하면 id_rsa.pub의 내용이

ssh-rsa ~~~

같은 형식으로 나타나는데 이를 끝까지 드래그해서 복사한다.

## 2. 복사한 ssh 키를 Github에 등록한다.

Github page->Settings->SSH keys-> SSH키 붙여넣고 등록해주면 된다!

이제 ssh 등록까지 완료!!!


# 4. ssh 키 잘 사용되는지 확인

git의 레파지토리 폴더로 들어가서 

```ssh -T git@github.com```

위의 명령어를 치면


```
The authenticity of host 'github.com (15.164.81.167)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```
yes를 입력하면 

```
Warning: Permanently added 'github.com,15.164.81.167' (RSA) to the list of known hosts.
Hi **name**! You've successfully authenticated, but GitHub does not provide shell access.
```
메세지가 뜨면 성공이다!

이제 로그인 없이 push가 잘 되는지 테스트까지 완료했다!

다들 ssh key 생성해서 github를 좀 더 쉽게 사용할 수 있도록 하자!
