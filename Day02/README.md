# Linux Study - Day02

## 📅 날짜

2026-07-20

---

# 오늘 배운 내용

## 1. 파일 권한(Permission)

리눅스는 User, Group, Others 세 가지 권한으로 관리된다.

### 권한 종류

| 문자 | 의미 |
|------|------|
| r | Read (읽기) |
| w | Write (쓰기) |
| x | Execute (실행) |

### 숫자 권한

| 숫자 | 권한 |
|------|------|
| 7 | rwx |
| 6 | rw- |
| 5 | r-x |
| 4 | r-- |
| 0 | --- |

### 실습

```bash
chmod 755 test.txt
chmod 644 test.txt
chmod 700 test.txt
```

### 내가 이해한 내용

- User는 파일의 소유자이다.
- Group은 같은 그룹에 속한 사용자이다.
- Others는 그 외 모든 사용자이다.
- 755는 rwx r-x r-x 이다.
- 644는 rw- r-- r-- 이다.

---

## 2. 사용자(User)

실습

```bash
whoami
id
groups
sudo whoami
```

### 배운 내용

- whoami : 현재 로그인한 사용자 확인
- id : UID, GID 확인
- groups : 현재 속한 그룹 확인
- sudo : 관리자(root) 권한으로 실행

---

## 3. 파일 검색

### find

```bash
find . -name "*.txt"
```

현재 폴더부터 txt 파일을 검색한다.

### grep

```bash
grep "unity" game.txt
```

파일 안에서 특정 문자열을 검색한다.

---

## 4. 프로세스

```bash
ps
ps -ef
top
kill PID
```

### 배운 내용

- ps : 현재 프로세스 확인
- top : 실시간 프로세스 확인
- kill : 프로세스 종료

---

# 오늘 느낀 점

처음에는 명령어를 외우는 공부라고 생각했는데,
직접 WSL에서 실습해보니 왜 사용하는지 이해할 수 있었다.

특히 chmod 권한과 grep, find 명령어가 재미있었다.

Git과 GitHub도 처음 연결해봤는데 생각보다 재미있었다.