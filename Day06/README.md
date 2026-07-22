# Linux Master 2급 Day06 - 패키지 관리

## 1. 패키지란?

패키지는 리눅스에서 프로그램을 설치하기 위한 파일 묶음이다.

윈도우의 설치 파일과 비슷하며, 프로그램 실행에 필요한 파일과 설정 정보를 포함한다.

---

## 2. 배포판별 패키지 관리

| 계열         | 대표 배포판                      | 패키지 형식 | 관리 명령어              |
| ---------- | --------------------------- | ------ | ------------------- |
| Red Hat 계열 | CentOS, Rocky Linux, Fedora | `.rpm` | `rpm`, `yum`, `dnf` |
| Debian 계열  | Ubuntu, Debian              | `.deb` | `dpkg`, `apt`       |

```text
Red Hat 계열 → rpm, yum, dnf
Debian 계열 → dpkg, apt
```

---

## 3. apt 명령어

`apt`는 Debian 계열에서 사용하는 패키지 관리 명령어이다.

인터넷 저장소에서 패키지를 다운로드하고, 필요한 의존성 패키지도 자동으로 설치한다.

### 패키지 목록 갱신

```bash
sudo apt update
```

설치 가능한 패키지 목록을 최신 상태로 갱신한다.

### 설치된 패키지 업그레이드

```bash
sudo apt upgrade
```

현재 설치된 패키지를 최신 버전으로 업그레이드한다.

### 패키지 설치

```bash
sudo apt install tree
```

### 패키지 삭제

```bash
sudo apt remove tree
```

프로그램은 삭제하지만 설정 파일은 남을 수 있다.

### 설정 파일까지 삭제

```bash
sudo apt purge tree
```

프로그램과 관련 설정 파일까지 삭제한다.

### 패키지 검색

```bash
apt search tree
```

### 패키지 정보 확인

```bash
apt show tree
```

---

## 4. dpkg 명령어

`dpkg`는 Debian 계열의 `.deb` 패키지 파일을 직접 관리하는 명령어이다.

`apt`와 달리 의존성을 자동으로 처리하지 못할 수 있다.

### deb 파일 설치

```bash
sudo dpkg -i package.deb
```

* `-i`: install

### 패키지 삭제

```bash
sudo dpkg -r 패키지명
```

* `-r`: remove

### 설치된 패키지 목록 조회

```bash
dpkg -l
```

* `-l`: list

### 특정 패키지 확인

```bash
dpkg -l | grep tree
```

설치된 패키지 목록 중 `tree`가 포함된 줄만 출력한다.

---

## 5. rpm 명령어

`rpm`은 Red Hat 계열의 `.rpm` 패키지를 직접 관리하는 명령어이다.

### 패키지 설치

```bash
rpm -i package.rpm
```

* `-i`: install

### 패키지 업그레이드

```bash
rpm -U package.rpm
```

* `-U`: upgrade

### 패키지 삭제

```bash
rpm -e 패키지명
```

* `-e`: erase

### 특정 패키지 조회

```bash
rpm -q 패키지명
```

* `-q`: query

### 설치된 모든 RPM 패키지 조회

```bash
rpm -qa
```

* `-q`: query
* `-a`: all

### 설치 진행 상황 표시

```bash
rpm -ivh package.rpm
```

* `-i`: 설치
* `-v`: 자세한 정보 출력
* `-h`: 진행 상황을 `#`으로 표시

---

## 6. yum과 dnf

`yum`과 `dnf`는 Red Hat 계열에서 저장소를 이용해 패키지를 관리하는 명령어이다.

```bash
yum install httpd
yum remove httpd
yum update
yum search httpd
```

최근 배포판에서는 `dnf`를 많이 사용한다.

```bash
dnf install httpd
```

---

## 7. apt와 dpkg 차이

| 구분     | apt                | dpkg               |
| ------ | ------------------ | ------------------ |
| 사용 계열  | Debian 계열          | Debian 계열          |
| 설치 방식  | 저장소에서 검색 및 설치      | `.deb` 파일 직접 설치    |
| 의존성 처리 | 자동 처리              | 직접 해결해야 할 수 있음     |
| 예시     | `apt install tree` | `dpkg -i tree.deb` |

---

## 8. rpm과 yum 차이

| 구분     | rpm                  | yum / dnf             |
| ------ | -------------------- | --------------------- |
| 사용 계열  | Red Hat 계열           | Red Hat 계열            |
| 설치 방식  | `.rpm` 파일 직접 설치      | 저장소에서 검색 및 설치         |
| 의존성 처리 | 직접 해결해야 할 수 있음       | 자동 처리                 |
| 예시     | `rpm -i package.rpm` | `yum install package` |

---

## 9. 핵심 비교

```text
rpm  ↔ dpkg
yum  ↔ apt
```

* `rpm`, `dpkg`: 패키지 파일 직접 관리
* `yum`, `dnf`, `apt`: 저장소를 이용한 패키지 관리

---

## 10. 핵심 명령어 정리

```bash
# Debian 계열
sudo apt update
sudo apt upgrade
sudo apt install 패키지명
sudo apt remove 패키지명
sudo apt purge 패키지명

dpkg -i package.deb
dpkg -r 패키지명
dpkg -l

# Red Hat 계열
rpm -i package.rpm
rpm -U package.rpm
rpm -e 패키지명
rpm -q 패키지명
rpm -qa
rpm -ivh package.rpm

yum install 패키지명
yum remove 패키지명
dnf install 패키지명
```

---

## 11. 오늘의 핵심 암기

```text
apt install → 저장소에서 설치
apt remove → 프로그램 삭제
apt purge → 설정 파일까지 삭제

dpkg -i → deb 파일 설치
dpkg -l → 설치된 패키지 목록

rpm -i → rpm 파일 설치
rpm -e → 패키지 삭제
rpm -q → 패키지 조회
rpm -qa → 모든 RPM 패키지 조회
```

## 학습 결과

* Debian 계열과 Red Hat 계열의 패키지 관리 방식을 구분할 수 있다.
* `apt`, `dpkg`, `rpm`, `yum`, `dnf`의 차이를 이해했다.
* 패키지 설치, 삭제, 조회 명령어를 사용할 수 있다.
* `remove`와 `purge`의 차이를 이해했다.
* `rpm -qa`, `rpm -e`, `dpkg -l`의 의미를 구분할 수 있다.
