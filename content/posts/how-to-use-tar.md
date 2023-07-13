---
title: "tar 명령어로 압축하고 푸는 방법"
description: "tar(.gz 포함) 파일을 압축하고 푸는 방법에 대해 기술합니다"
date: 2023-07-13
draft: false
categories:
  - linux
tags:
  - 압축
  - 명령어
  - tar
  - tar.gz
authorbox: true
---

## 들어가며

tar 파일을 압축하고 푸는 명령어를 자꾸 까먹어서 기록으로 남깁니다.

## 문법과 예제

### tar 압축하기

- 문법
    ```text
    > tar -cf <저장할 파일명> <압축대상 파일(* 사용 가능)>
    ```
- 예제 : 현재 디렉토리의 **모든 파일들**을 **my_data.tar** 파일로 압축합니다.
    ```sh
    > tar -cf my_data.tar *
    ```

### tar 압축풀기

- 문법
    ```text
    > tar -xf <압축된 파일명>
    ```
- 예제 : 현재 디렉토리의 **my_data.tar** 압축파일을 현재 디렉토리에 풉니다.
    ```sh
    > tar -xf my_data.tar
    ```

### tar.gz 압축하기

- 문법
    ```text
    > tar -zcf <저장할 파일명> <압축대상 파일(* 사용 가능)>
    ```
- 예제 : 현재 디렉토리의 **모든 파일들**을 **my_data.tar.gz** 파일로 압축합니다.
    ```sh
    > tar -zcf my_data.tar.gz *
    ```

### tar.gz 압축풀기

- 문법
    ```text
    > tar -zxf <압축된 파일명>
    ```
- 예제 : 현재 디렉토리의 **my_data.tar.gz** 압축파일을 현재 디렉토리에 풉니다.
    ```sh
    > tar -zxf my_data.tar.gz
    ```

## 참고

### 자주 사용되는 tar 옵션별 설명
| 옵션 | 설명 |
|-|-|
| c | tar 압축하기 |
| f | 파일 이름을 지정 |
| p | 파일 권한을 보존 |
| v | 처리 과정을 콘솔에 출력 |
| x | tar 압축풀기 |
| z | gzip 처리 적용 |

### `tar --help` 출력 내용
```
tar(bsdtar): manipulate archive files
First option must be a mode specifier:
  -c Create  -r Add/Replace  -t List  -u Update  -x Extract
Common Options:
  -b #  Use # 512-byte records per I/O block
  -f <filename>  Location of archive
  -v    Verbose
  -w    Interactive
Create: tar -c [options] [<file> | <dir> | @<archive> | -C <dir> ]
  <file>, <dir>  add these items to archive
  -z, -j, -J, --lzma  Compress archive with gzip/bzip2/xz/lzma
  --format {ustar|pax|cpio|shar}  Select archive format
  --exclude <pattern>  Skip files that match pattern
  -C <dir>  Change to <dir> before processing remaining files
  @<archive>  Add entries from <archive> to output
List: tar -t [options] [<patterns>]
  <patterns>  If specified, list only entries that match
Extract: tar -x [options] [<patterns>]
  <patterns>  If specified, extract only entries that match
  -k    Keep (don't overwrite) existing files
  -m    Don't restore modification times
  -O    Write entries to stdout, don't restore to disk
  -p    Restore permissions (including ACLs, owner, file flags)
```