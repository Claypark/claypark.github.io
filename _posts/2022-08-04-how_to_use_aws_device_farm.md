---
title: "How to use AWS device farm."
date: 2022-08-04 14:10:00 +0900
categories: aws
tags:
- aws
- ios
---

- 전제 조건: AWS 가입자, Device farm 추가.

프로젝트 생성
---------

- iPhone slot을 추가시키고 나서 purchase 버튼 클릭 (구매 필요함)
- Create a new project - project name 입력.

Test 생성
---------

- 한 번의 테스트 실행을 위해 아래의 과정을 거쳐야 한다. 테스트 할때마다 진행해줘야 된다.
  - Create a new run
  - Choose your application
    - 사과모양 클릭 - 테스트할 앱의 .ipa 파일 업로드 - 이름 입력하기
  - Configure your test
    - Test는 XCTest UI 선택. upload file에 {PROJECT_NAME}_Runner.ipa 를 첨부한다.
      - Runner.ipa 만들려면
        - 'Payload' 이름으로 디렉토리 생성.
        - DerivedData/.../Debug-iphoneos/Products/ 내의 .app 파일을 Payload 디렉토리안에 넣는다.
        - Payload 디렉토리를 zip으로 압축하고, 확장자를 ipa로 바꾼다.
    - Choose your execution environment에서 
      - 기본 환경설정으로 테스트하려면 **Run your test in our standard environment** 체크
      - 커스텀하게 테스트 하려면 **Run your test in a custom**체크 후 스크립트를 수정하면 된다.
  - Select Device
    - 테스트하기 원하는 Device pool을 선택한다.
  - Specify device state
    - 추가적인 디바이스 상태들을 여기에 입력한다. 다른앱을 install하기 원하는 경우 install other apps에 추가하면 된다.

