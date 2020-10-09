## SSH

[[Git (7)] Github 비밀번호 입력 없이 pull/push 하기(github ssh key 설정)](https://goddaehee.tistory.com/254)

**1) SSH(Secure Shell Protocol)**

- 암호화된 원격 접속 프로토콜

- 즉 컴퓨터와 컴퓨터가 인터넷과 같은 Public Network를 통해 서로 통신을 할 때 보안적으로 안전하게 통신을 하기 위해 사용하는 접속 프로토콜

**2) SSH Key**

- SSH 프로토콜로 서버에 접속 시 서버에 비밀번호 대신 key를 제출하는 방식이다.

### 과정

- ssh 경로가 없는 경우 추가

```bash
mkdir ~/.ssh 
chmod 700 ~/.ssh 
cd ~/.ssh

```

- ssh key 생성

```bash
ssh-keygen -t rsa -b 4096 -C "yourEmail@example.com"
```

- -t rsa는 rsa라는 암호화 방식으로 키를 생성한다는 의미다.
- SSH 키는 키 크기가 2048비트 또는 4096비트인 RSA 키여야 한다. 나와 같은 경우는 4096으로 지정하였다.

```bash
#특정 경로 지정이 필요한 경우 절대 경로 입력하면 적용 가능하다. 엔터치면 디폴트 경로
Generating public/private rsa key pair. 
Enter file in which to save the key (/home/user/.ssh/id_rsa):

#자동 로그인을 사용하려면 입력하지 않고 엔터
Enter passphrase (empty for no passphrase): 
Enter same passphrase again:

#비밀번호 변겅
ssh-keygen -p
```

- 생성 결과
    - **authorized_keys:** id_rsa.pub 키의 값을 저장 한다.
    - **id_rsa : 개인키**
    - **id_rsa.pub : 공개키**

- 실행 확인

```bash
eval "$(ssh-agent -s)" 
Agent pid xxxx
```

- SSH-Agent에 SSH Key 등록

```bash
ssh-add ~/.ssh/id_rsa 
Enter passphrase for /root/.ssh/id_rsa: 
Identity added: /root/.ssh/id_rsa (/root/.ssh/id_rsa)

```

- GitHub Setting에서 SSH key 등록
    - cat ~/.ssh/id_rsa.pub 복사하여 등록
- Repo - Clone or Download (Code) 에서 SSH URL복사
- origin 등록

```bash
# 이미 origin 있다면 제거후 등록
git remote remove origin

git remote add origin git@github.com:[계정명]/[저장소명].git
```

## Bash

```bash
#crontab -e
*/5 * * * * ~/deploy.sh
```

```bash
#~/deploy.sh
#!/bin/bash
cd ~/javascript-w5-accountbook/ #git repo로 이동해야 git 명령어 사용가능
git fetch origin dev
origin=$(git rev-parse remotes/origin/dev)
master=$(git rev-parse HEAD)
if [ ${origin} != ${master} ]; then
	git pull origin dev
  #node 와 pm2경로를 지정해줘야 동작한다
	/root/.nvm/versions/node/v14.12.0/bin/node /root/.nvm/versions/node/v14.12.0/bin/pm2 restart 0
	echo auto deploy at >> ../output.txt
	date >> ../output.txt
fi
```