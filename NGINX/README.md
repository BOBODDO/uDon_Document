# NGINX 도큐먼트

## 구현 목표

11/13일 회의에서 의논한 바와 같이 아래와 같이 구현합니다.</br>

> 1. 각 유저 별 서버 계정 별도 생성</br>
> 2. 각 유저 별 서브 도메인 발급 및 연결</br>
>    server.[유저이름].udon.com : 서버 접속</br> > [유저이름].udon.com : 클라이언트 접속(고객에게 보여지는 화면)</br>

## **유저 디렉토리 구조(서버 셋팅 구조)**

### **client 디렉토리**

> /home/[유저이름]/client

위 경로는 [유저이름].udon.com 으로 접속 시 보여주어야 하는 컨텐츠들이 담길 공간입니다.

index.html 등 이 위치합니다.

### **server 디렉토리**

> /home/[유저이름]/server

위 경로는 server.[유저이름].udon.com 와 관련되어 있으나, 보여주어야 하는 컨텐츠들이 담길 공간은 아닙니다.

server.[유저이름].udon.com 접속 시 nginx는 내부 설정에 따라 서버의 포트로 proxy_pass 를 진행합니다.

각 유저들은 해당 폴더에서 node.js 모듈 설치 및 구동을 해주시면 되며, 단 포트는 서로 다른 유저 간에 중복되지 않도록 적절히 수정이 필요합니다.

## **nginx 설정 디렉토리 구조**

### **snippets 디렉토리**

각종 설정 파일들 (보안 등)이 담길 폴더

### **sites 디렉토리**

각 도메인 별 설정 파일이 담길 폴더

nginx 설정 파일 구문은 본 디렉토리의 하위 디렉토리 'CONF 파일' 에 .CONF 형태로 저장해놓겠습니다.

해당 CONF 파일을 서버의 (예: /etc/nginx/..) 경로에 올바르게 위치시킨 후

> systemctm nginx reload

명령어를 통해 설정 파일은 nginx 에 반영시켜 주세요.