# Day05 - 파일 검색 / 문자열 검색 / 복사 / 이동 / 삭제

## find - 파일 및 디렉터리 검색

이름으로 검색
```bash
find . -name "*.txt"

파일만 검색

find . -type f

디렉터리만 검색

find . -type d

조건 조합

find . -type f -name "*.txt"
grep - 파일 내용에서 문자열 검색
grep "linux" note.txt
cp - 복사

파일 복사

cp file1.txt file2.txt

디렉터리 복사

cp -r images images_backup
mv - 이동 / 이름 변경

이름 변경

mv old.txt new.txt

파일 이동

mv test.txt backup/
rm - 삭제

파일 삭제

rm test.txt

디렉터리와 내부 내용 삭제

rm -r directory
핵심 정리
find : 파일/디렉터리 찾기
-name : 이름 조건
-type f : 파일만
-type d : 디렉터리만
grep : 문자열 검색
cp : 복사
cp -r : 디렉터리 복사
mv : 이동 또는 이름 변경
rm : 파일 삭제
rm -r : 디렉터리 삭제