# 도커 쿠버네티스 워크샵

## Contents

1. [도커 실행](01/01.md)
2. [도커 레지스트리](01/02.md)
3. [Dockerfile 작성 및 빌드](01/03.md)
4. [MSA container](01/04.md)

## 실습환경

- OS: ubuntu 18.04
- root user (sudo)
- CPU 2 core / MEM 4G / Disk 50G
- Public IP 권장 (EC2 / GCE / Azure VM)

## 사전지식

- 리눅스 기본 지식이 필요합니다. (ssh, vim, apt, curl 등)
- 간단한 프로그래밍 지식을 요구합니다. 언어는 무관하지만 이 책에서는 파이썬을 주로 다룹니다. 파이썬을 모르시더라도 전반적인 프로그래밍 지식만으로도 충분히 이해할 수 있습니다.
- 간단한 클라우드 지식이 필요합니다.
- `tmux`, `screen`과 같은 터미널 멀티플랙서를 사용하면 편리합니다.


## 서버 접속

리눅스 서버로 접속할 터미널을 윈도우 서버에 설치합니다. `putty` ([https://www.putty.org](https://www.putty.org/)) 등 선호하는 터미널을 사용해도 무방합니다.

1. MobaXterm 다운로드: [https://mobaxterm.mobatek.net/download.html](https://mobaxterm.mobatek.net/download.html)
2. `Home Edition` > `Download now` 클릭
3. `MobaXterm Home Edition (Portable edition)` 다운로드
4. 다운로드 완료된 파일 압축 해제
5. `Session` 버튼 > `SSH` 버튼 클릭
6. Remote host / User 입력
7. (Optional) Advanced SSH settings > Use private key (체크) > PEM키 등록

![[그림 3-3] MobaXterm](01.png)
