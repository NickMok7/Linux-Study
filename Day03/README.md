# Linux Study - Day03

## 📅 날짜

2026-07-20

---

# 오늘 배운 내용

## 1. 파일 압축

리눅스에서는 `tar`로 파일이나 폴더를 하나로 묶고, `gzip`으로 압축할 수 있다.

### tar로 묶기

```bash
tar -cvf compress-test.tar compress-test
```

### tar 풀기

```bash
tar -xvf compress-test.tar
```

### gzip 압축

```bash
gzip compress-test.tar
```

### gzip 압축 해제

```bash
gunzip compress-test.tar.gz
```

### tar + gzip 함께 사용

```bash
tar -czvf backup.tar.gz project
```

### tar.gz 압축 해제

```bash
tar -xzvf backup.tar.gz
```

### 옵션

| 옵션 | 의미 |
|------|------|
| c | Create (생성) |
| x | Extract (압축 해제) |
| z | gzip 압축 |
| v | Verbose (진행 과정 출력) |
| f | File (파일 이름 지정) |

---

# 2. 디스크 용량 확인

### 디스크 전체 용량 확인

```bash
df
```

### 사람이 보기 편한 단위로 출력

```bash
df -h
```

### 파일 및 디렉터리 용량 확인

```bash
du
```

### 사람이 보기 편한 단위

```bash
du -h
```

### 현재 폴더 용량만 요약

```bash
du -sh
```

### 배운 내용

- df : 디스크 전체 용량 확인
- du : 파일 및 디렉터리 용량 확인
- -h : 사람이 읽기 쉬운 단위(KB, MB, GB)
- -s : Summary(요약)

---

# 3. 네트워크 명령어

### 컴퓨터 이름 확인

```bash
hostname
```

### 네트워크 연결 확인

```bash
ping google.com
```

> 종료 : Ctrl + C

### IP 주소 확인

```bash
ip addr
```

또는

```bash
ip a
```

### 배운 내용

- hostname : 컴퓨터 이름 확인
- ping : 네트워크 연결 상태 및 응답속도 확인
- ip addr : 현재 IP 주소 확인

---

# 오늘 정리

## 압축

- tar : 파일이나 폴더를 하나로 묶음
- gzip : 파일 압축
- gunzip : gzip 압축 해제

## 디스크

- df : 디스크 전체 용량
- du : 파일 및 디렉터리 용량

## 네트워크

- hostname : 컴퓨터 이름
- ping : 네트워크 연결 확인
- ip addr : IP 주소 확인