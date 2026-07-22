# Linux Master 2급 Day07 - 네트워크 명령어

## 1. 네트워크 명령어 개요

리눅스에서는 명령어를 이용해 다음과 같은 작업을 할 수 있다.

* 내 컴퓨터의 IP 주소 확인
* 다른 서버와의 연결 상태 확인
* 열려 있는 포트 확인
* 도메인과 IP 주소 확인
* 원격 서버 접속
* 인터넷에서 파일 다운로드

---

## 2. `hostname`

현재 컴퓨터의 호스트 이름을 확인한다.

```bash
hostname
```

호스트 이름은 네트워크에서 컴퓨터를 구분하기 위한 이름이다.

### IP 주소 빠르게 확인

```bash
hostname -I
```

현재 컴퓨터에 할당된 IP 주소를 간단하게 확인할 때 사용한다.

```text
hostname    → 컴퓨터 이름 확인
hostname -I → 내 IP 주소 빠르게 확인
```

---

## 3. `ip addr`

네트워크 인터페이스와 IP 주소를 자세히 확인한다.

```bash
ip addr
```

짧게 작성할 수도 있다.

```bash
ip a
```

출력 예시:

```text
2: eth0
    inet 172.20.10.5/20
```

* `eth0`: 네트워크 인터페이스 이름
* `inet`: IPv4 주소
* `172.20.10.5`: 현재 IP 주소
* `/20`: 서브넷 정보

```text
IP만 빠르게 확인       → hostname -I
네트워크 정보를 자세히 확인 → ip addr
```

---

## 4. `ifconfig`

네트워크 인터페이스와 IP 주소를 확인하는 전통적인 명령어이다.

```bash
ifconfig
```

최신 리눅스에서는 `ifconfig`보다 `ip addr`를 주로 사용한다.

Ubuntu에 설치되어 있지 않다면 다음 패키지를 설치한다.

```bash
sudo apt install net-tools
```

```text
예전 방식 → ifconfig
최신 방식 → ip addr
```

---

## 5. `ping`

상대 컴퓨터나 서버와 네트워크 통신이 가능한지 확인한다.

```bash
ping google.com
```

기본적으로 계속 실행되며 `Ctrl + C`로 종료한다.

### 횟수를 지정하여 실행

```bash
ping -c 4 google.com
```

* `-c`: 패킷 전송 횟수 지정
* `4`: 총 4번 전송

IP 주소로 인터넷 연결 자체를 확인할 수도 있다.

```bash
ping -c 4 8.8.8.8
```

```text
상대 서버와 연결되는지 확인 → ping
```

단, 서버에서 보안 설정으로 ping 응답을 차단할 수도 있으므로 ping 실패가 반드시 서버 장애를 의미하지는 않는다.

---

## 6. `ss`

현재 네트워크 연결과 열려 있는 포트를 확인한다.

```bash
ss
```

### 대기 중인 TCP 포트를 숫자로 확인

```bash
ss -lnt
```

옵션 의미:

* `-l`: LISTEN 상태만 출력
* `-n`: 주소와 포트를 숫자로 출력
* `-t`: TCP만 출력

```text
ss -lnt → 현재 연결을 기다리는 TCP 포트 확인
```

### 모든 TCP 연결 확인

```bash
ss -ant
```

* `-a`: 모든 연결
* `-n`: 숫자로 출력
* `-t`: TCP

### 특정 포트 확인

```bash
ss -lnt | grep 22
```

SSH 기본 포트인 22번 포트가 열려 있는지 확인할 수 있다.

---

## 7. `netstat`

`ss`와 비슷하게 네트워크 연결 상태와 포트를 확인한다.

```bash
netstat -lnt
```

최근에는 `netstat`보다 `ss`를 주로 사용한다.

```text
예전 방식 → netstat
최신 방식 → ss
```

Ubuntu에서 명령어가 없다면 다음 패키지를 설치한다.

```bash
sudo apt install net-tools
```

---

## 8. 주요 포트 번호

포트는 하나의 컴퓨터 안에서 어떤 서비스와 통신할지를 구분하는 번호이다.

| 서비스   | 포트 번호 |
| ----- | ----: |
| FTP   |    21 |
| SSH   |    22 |
| DNS   |    53 |
| HTTP  |    80 |
| HTTPS |   443 |

```text
IP 주소   → 건물 주소
포트 번호 → 건물 안의 방 번호
```

예:

```text
192.168.0.10:22
```

`192.168.0.10` 서버의 SSH 서비스에 접속한다는 의미이다.

---

## 9. `nslookup`

도메인 이름이 어떤 IP 주소로 연결되는지 확인한다.

```bash
nslookup google.com
```

DNS가 정상적으로 작동하는지 확인할 때 사용할 수 있다.

```text
도메인의 IP 주소 확인 → nslookup
```

Ubuntu에 설치되어 있지 않다면 다음 패키지를 설치한다.

```bash
sudo apt install dnsutils
```

---

## 10. `traceroute`

내 컴퓨터에서 목적지 서버까지 거치는 네트워크 경로를 확인한다.

```bash
traceroute google.com
```

네트워크 통신은 여러 라우터를 거쳐 목적지에 도착한다.

```text
내 컴퓨터
→ 공유기
→ 통신사 네트워크
→ 중간 라우터
→ 목적지 서버
```

### 사용 목적

* 특정 사이트만 느릴 때
* 어느 네트워크 구간에서 문제가 발생하는지 확인할 때
* 목적지까지 거치는 경로를 확인할 때

```text
연결 여부 확인 → ping
이동 경로 확인 → traceroute
```

Ubuntu에 설치되어 있지 않다면 다음 패키지를 설치한다.

```bash
sudo apt install traceroute
```

---

## 11. `curl`

웹 서버나 API에 요청을 보내고 응답을 확인한다.

```bash
curl https://example.com
```

웹페이지의 HTML 내용이 터미널에 출력된다.

### HTTP 응답 헤더 확인

```bash
curl -I https://example.com
```

### 파일 다운로드

원래 파일 이름으로 저장:

```bash
curl -O https://example.com/file.zip
```

직접 이름을 지정하여 저장:

```bash
curl -o test.zip https://example.com/file.zip
```

```text
-O → 원래 파일 이름으로 저장
-o → 저장할 파일 이름 직접 지정
```

### 사용 목적

* 웹 서버 작동 확인
* API 응답 확인
* HTTP 상태 및 헤더 확인
* 간단한 파일 다운로드

```text
웹 서버에 요청하고 응답 확인 → curl
```

---

## 12. `wget`

인터넷에서 파일을 다운로드할 때 사용한다.

```bash
wget https://example.com/file.zip
```

다른 이름으로 저장하려면:

```bash
wget -O test.zip https://example.com/file.zip
```

```text
curl → 웹 서버 요청과 응답 확인
wget → 파일 다운로드
```

---

## 13. `ssh`

다른 리눅스 컴퓨터나 서버에 원격으로 접속한다.

```bash
ssh 사용자명@IP주소
```

예:

```bash
ssh nick@192.168.0.10
```

AWS 서버에 접속하는 예:

```bash
ssh ubuntu@서버IP
```

특정 포트로 접속하려면:

```bash
ssh -p 2222 nick@192.168.0.10
```

SSH의 기본 포트는 `22번`이다.

```text
원격 서버의 터미널에 접속 → ssh
```

---

## 14. `scp`

SSH를 이용해 내 컴퓨터와 원격 서버 사이에서 파일을 복사한다.

### 내 컴퓨터의 파일을 서버로 전송

```bash
scp hello.txt nick@192.168.0.10:/home/nick/
```

### 서버의 파일을 내 컴퓨터로 가져오기

```bash
scp nick@192.168.0.10:/home/nick/hello.txt .
```

마지막의 `.`은 현재 디렉터리를 의미한다.

### 디렉터리 전체 복사

```bash
scp -r project nick@192.168.0.10:/home/nick/
```

* `-r`: 디렉터리 내부까지 재귀적으로 복사

```text
원격 서버 접속       → ssh
원격 서버와 파일 복사 → scp
```

---

## 15. 핵심 명령어 비교

| 상황              | 명령어           |
| --------------- | ------------- |
| 컴퓨터 이름 확인       | `hostname`    |
| 내 IP 빠르게 확인     | `hostname -I` |
| 네트워크 장치와 IP 확인  | `ip addr`     |
| 예전 방식의 네트워크 확인  | `ifconfig`    |
| 상대 서버와 연결 확인    | `ping`        |
| 열린 포트 확인        | `ss`          |
| 예전 방식의 포트 확인    | `netstat`     |
| 도메인의 IP 주소 확인   | `nslookup`    |
| 목적지까지의 경로 확인    | `traceroute`  |
| 웹 서버나 API 응답 확인 | `curl`        |
| 인터넷에서 파일 다운로드   | `wget`        |
| 원격 서버 접속        | `ssh`         |
| 원격 서버와 파일 복사    | `scp`         |

---

## 16. 네트워크 장애 점검 순서

### 1단계: IP 주소 확인

```bash
ip addr
```

현재 컴퓨터에 IP 주소가 정상적으로 할당되어 있는지 확인한다.

### 2단계: 인터넷 연결 확인

```bash
ping -c 4 8.8.8.8
```

IP 주소를 이용해 외부 인터넷과 통신이 가능한지 확인한다.

### 3단계: DNS 확인

```bash
nslookup google.com
```

도메인 이름이 정상적으로 IP 주소로 변환되는지 확인한다.

### 4단계: 도메인 통신 확인

```bash
ping -c 4 google.com
```

도메인 이름을 이용한 통신이 가능한지 확인한다.

### 5단계: 네트워크 경로 확인

```bash
traceroute google.com
```

목적지까지 어느 구간을 거치며 어디서 문제가 발생하는지 확인한다.

---

## 17. 서버 접속 장애 점검

서버 접속이 되지 않을 때 다음 순서로 확인할 수 있다.

### 서버까지 연결되는지 확인

```bash
ping 서버IP
```

### 서버에서 포트가 열려 있는지 확인

```bash
ss -lnt
```

### 웹 서비스가 응답하는지 확인

```bash
curl http://서버IP:포트
```

```text
통신 확인       → ping
포트 확인       → ss
서비스 응답 확인 → curl
```

---

## 18. 핵심 암기

```text
IP 확인      → hostname -I, ip addr
연결 확인    → ping
포트 확인    → ss -lnt
DNS 확인     → nslookup
경로 확인    → traceroute
웹 응답 확인 → curl
파일 다운로드 → wget
원격 접속    → ssh
원격 복사    → scp
```

한 줄 암기:

```text
IP는 ip, 연결은 ping, 포트는 ss, DNS는 nslookup, 경로는 traceroute
```

---

## 19. 학습 결과

* 호스트 이름과 IP 주소를 확인할 수 있다.
* 네트워크 연결 상태를 확인할 수 있다.
* 현재 열려 있는 TCP 포트를 확인할 수 있다.
* 도메인과 IP 주소의 관계를 확인할 수 있다.
* 목적지까지의 네트워크 경로를 확인할 수 있다.
* 웹 서버와 API의 응답을 확인할 수 있다.
* 원격 서버에 접속하고 파일을 복사할 수 있다.
