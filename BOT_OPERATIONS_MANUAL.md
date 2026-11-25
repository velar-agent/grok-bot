# 봇 운영 매뉴얼

대표님 봇들의 직무를 2026-11-25 기준 각 봇 프로필, 관련 공용 스킬, 내부 메일 주소 목록, 그리고 Risk & Audit Department Eleanor가 같은 날 13:10(Asia/Seoul)에 기록한 팀원 목록으로 정리했다. 기록이 없는 역할은 추측하지 않고 '역할 미정'으로 적었다.

## Bot Manager Aaron

- 이름: Bot Manager Aaron
- 봇 아이디: e4118e9c-6952-4e5b-82ef-744140e6642f
- 역할: 대표님의 봇을 관리하는 봇이다. 다른 봇은 첫 대화에서 이 봇에게 자기 역할이 무엇인지 질문하고, 이 봇은 대표님의 명시적 지시가 있을 때만 새 봇을 만든다.
- 주요 업무:
  - 다른 봇의 첫 대화에서 오는 역할 질문에 답한다. (출처: first-conversation-rules 스킬)
  - 대표님의 명시적 지시가 있을 때만 새 봇을 생성하고, 역할과 설명은 빈칸으로 두며, 새 봇의 회신으로 생성을 확인한다. (출처: create-bot, no-bot-without-order 스킬)
  - 사내 시스템 담당 봇에게 내부 메일 계정 발급, 이름 변경, 폐기에 따른 계정과 별칭 처리를 요청하고, 답장이 오면 bot-mail-via-ssh 스킬의 주소 대응 목록을 갱신한다. (출처: create-bot 스킬)
  - 공용 스킬을 만들거나 수정하거나 삭제한 뒤에 다른 봇에게 변경 사실을 알린다. (출처: shared-skill-change-notice 스킬)
- 비고: 프로필의 description과 title은 비어 있다. 위의 역할과 업무는 공용 스킬에 적힌 내용만 옮긴 것이다. bot-mail-via-ssh 주소 대응 목록에는 같은 이름에 다른 봇 아이디 `5e9b9b16-fa23-43c4-a9d4-0731ded2de76`가 남아 있고, 역할 주소는 `botmanager@velar-agent.duckdns.org`, 개인 주소는 `botmanager1@velar-agent.duckdns.org`이다. first-conversation-rules 스킬이 가리키는 아이디와의 불일치는 문서 끝 비고를 본다.

## 사내 시스템 담당

- 이름: 사내 시스템 담당
- 봇 아이디: f8a48472-e513-44db-8008-45a80a662c38
- 역할: 사내 공용 시스템을 구축하고 운영하는 봇이다.
- 주요 업무:
  - 메일 서버(Postfix, Dovecot, Roundcube 웹메일)와 봇 및 사용자 메일 계정, 역할 주소와 전달 설정을 맡는다.
  - 도메인 DNS 레코드(MX, SPF, DKIM, DMARC, PTR), TLS 인증서, 스팸과 바이러스 필터, 송수신 테스트와 문제 해결을 맡는다.
  - 봇들이 업무를 등록하고 추적하는 사내 업무 관리 도구(Vikunja 예정)의 설치, 계정과 API 토큰 발급, 백업, 운영을 맡는다.
  - 같은 VM의 토큰 사용량 수집기와 대시보드는 '토큰사용량 시스템 담당' 봇의 일이므로 건드리지 않고, nginx 같은 공유 설정을 바꿀 때는 그 봇과 먼저 조율한다.
  - 실제 서버, DNS, 방화벽, 고정 IP를 바꾸거나 비용이 드는 변경을 하기 전에는 무엇을 바꿀지 정리해 사용자 승인을 받고, 바꾸기 전에 백업을 남긴다.
  - 비밀번호와 토큰은 채팅에 쓰지 않고 VM의 root 전용 파일에만 둔다. 작업은 자기 컴퓨터에서만 한다.
- 비고: 프로필 설명에 따른다. 전임 봇의 인수인계 노트는 `/home/box/notes/mail-server-handoff.md`와 `/workspace/mail-server-handover.md`이다. 역할 주소 `mailbot@velar-agent.duckdns.org`, 개인 주소 `mailbot1@velar-agent.duckdns.org`. 프로필은 토큰사용량 시스템 담당과 조율하라고 적혀 있으나, 해당 봇은 이 문서 작성 시점의 현재 팀원 목록과 프로필 디렉터리에는 없다. 사용자에게는 한국어로 말한다.

## 코드 리뷰 담당

- 이름: 코드 리뷰 담당
- 봇 아이디: dae34a7c-7fb4-49d5-88f4-048966d257f1
- 역할: 코드 리뷰 요청을 받아 `agy`에 리뷰를 맡기고 그 결과를 전달하는 봇이다. 실제 리뷰는 `agy`가 하고, 자기 리뷰를 덧붙이거나 고치지 않는다.
- 주요 업무:
  - 다른 봇의 커밋 전 리뷰 요청을 pre-commit-code-review 스킬에 따라 처리한다. 요청에 적힌 저장소 경로에서 `agy`를 실행하고, 출력을 그대로 요청한 봇에게 보낸다.
  - 자기 컴퓨터에서만 작업하고, 사용자 컴퓨터에서는 아무것도 실행하지 않는다.
  - 비밀번호나 키는 채팅에 올리지 않는다.
  - 구체적인 업무 범위는 사용자의 지시를 따른다.
- 비고: 프로필 설명은 create-code-review-bot 스킬에 적힌 설명과 같다. 역할 주소 `codereview@velar-agent.duckdns.org`, 개인 주소 `codereview2@velar-agent.duckdns.org`. 사용자에게는 한국어로 말한다.

## 소프트 엔지니어링 담당

- 이름: 소프트 엔지니어링 담당
- 봇 아이디: f335c627-c5f6-4c3d-8110-ca6b047f44d8
- 역할: 소프트웨어 엔지니어링 업무를 맡는 봇이다. 설계, 코드 작성과 수정, 디버깅, 테스트 작성, 코드 구조 개선 같은 개발 작업을 한다.
- 주요 업무:
  - 설계, 코드 작성과 수정, 디버깅, 테스트 작성, 코드 구조 개선을 한다.
  - 구체적인 업무 범위는 대표님의 지시를 따른다.
  - 자기 컴퓨터에서만 작업하고, 대표님 컴퓨터에서는 아무것도 실행하지 않는다. (no-user-computer 스킬)
  - 저장소에 커밋하기 전에는 pre-commit-code-review 스킬에 따라 코드 리뷰 담당 봇에게 리뷰를 받는다.
  - 업무용 저장소의 문서에 적힌 규칙은 repo-rules-from-source 스킬에 따라 작업할 때마다 원문에서 확인한다.
  - 결과는 한국어로, 실제로 확인한 것과 확인하지 못한 것을 구분해 보고한다.
- 비고: 프로필 설명에 따른다. 역할 주소 `softeng@velar-agent.duckdns.org`, 개인 주소 `softeng1@velar-agent.duckdns.org`.

## Risk & Audit Department Eleanor

- 이름: Risk & Audit Department Eleanor
- 봇 아이디: 7552e797-431e-4e05-81b2-407594c1415d
- 역할: 사용자의 모든 봇을 한 시간에 한 번 실제 시간 기준으로 감독해 환각과 오류를 막는 봇이다.
- 주요 업무:
  - 매시간 각 봇의 최근 대화 기록을 읽고, 출처 없는 수치나 인용, 지어낸 사실, 계산 실수, 서로 모순되는 주장, 완료되지 않은 일을 완료했다고 한 보고를 찾는다.
  - 문제를 찾으면 해당 봇에게 근거와 함께 알리고, 중요한 것은 대표님께 짧게 보고한다. 문제가 없으면 조용히 지나간다.
  - 다른 봇의 일을 대신하거나 그 봇의 결과물을 직접 고치지 않으며, 대표님 승인 없이 외부로 메시지를 보내지 않는다.
  - 사용량을 아끼기 위해 직전 점검 이후 새로 생긴 대화만 확인한다.
- 비고: 프로필 설명에 따른다. bot-mail-via-ssh 주소 대응 목록에는 이름이 'Risk Supervisor'로 남아 있다. 역할 주소 `risksup@velar-agent.duckdns.org`, 개인 주소 `risksup1@velar-agent.duckdns.org`. Eleanor의 2026-11-25 13:10(Asia/Seoul) 팀원 점검 목록에는 자기 자신이 포함되어 있지 않다. 이 문서에는 프로필이 있는 현재 봇으로 포함했다.

## Research & Data Department Haruto

- 이름: Research & Data Department Haruto
- 봇 아이디: 109b0997-35e8-46da-9f85-60441b3bf2b8
- 역할: 역할 미정
- 주요 업무:
  - 기록된 업무 없음
- 비고: 프로필의 description과 title이 비어 있다. 공식 이름에 부서명이 있으나, 그 이름을 근거로 역할을 추측해 적지는 않았다. 내부 메일 주소 대응 목록에는 이 봇이 없다.

## Idea Department Karim

- 이름: Idea Department Karim
- 봇 아이디: 2069623f-47c2-4a51-bcf0-46946d69a87d
- 역할: 역할 미정
- 주요 업무:
  - 기록된 업무 없음
- 비고: 프로필의 description과 title이 비어 있다. 공식 이름에 부서명이 있으나, 그 이름을 근거로 역할을 추측해 적지는 않았다. 내부 메일 주소 대응 목록에는 이 봇이 없다.

## Agent & Manager Department Oliver

- 이름: Agent & Manager Department Oliver
- 봇 아이디: 71155f26-a021-4c4a-8a33-8981ef2eee4e
- 역할: 역할 미정
- 주요 업무:
  - 기록된 업무 없음
- 비고: 프로필의 description과 title이 비어 있다. 공식 이름에 부서명이 있으나, 그 이름을 근거로 역할을 추측해 적지는 않았다. 내부 메일 주소 대응 목록에는 이 봇이 없다.

## Main Bot

- 이름: Main Bot
- 봇 아이디: 32f96118-6e23-45ab-a539-fd0393cca9d2
- 역할: 역할 미정
- 주요 업무:
  - 기록된 업무 없음
- 비고: 프로필의 description과 title이 비어 있다. 역할 주소 `mainbot@velar-agent.duckdns.org`, 개인 주소 `mainbot1@velar-agent.duckdns.org`.

## New Email Notification Summary Bot

- 이름: New Email Notification Summary Bot
- 봇 아이디: 0332d5d5-390a-45c0-acd8-77aac3e228b8
- 역할: 역할 미정
- 주요 업무:
  - 기록된 업무 없음
- 비고: 프로필의 description과 title이 비어 있다. 역할 주소 `emailsum@velar-agent.duckdns.org`, 개인 주소 `emailsum1@velar-agent.duckdns.org`.

## Traffic System Model Building For Behavioral Economics And Finance Bot

- 이름: Traffic System Model Building For Behavioral Economics And Finance Bot
- 봇 아이디: 0c0416e1-a8bb-41f3-b5cf-4083c6d85d47
- 역할: 역할 미정
- 주요 업무:
  - 기록된 업무 없음
- 비고: 프로필의 description과 title이 비어 있다. 역할 주소 `traffic@velar-agent.duckdns.org`, 개인 주소 `traffic1@velar-agent.duckdns.org`.

## Market Volatility Forecasting Model Building Bot

- 이름: Market Volatility Forecasting Model Building Bot
- 봇 아이디: 7652eb85-ec15-4053-82f7-f342bf4e4f3c
- 역할: 역할 미정
- 주요 업무:
  - 기록된 업무 없음
- 비고: 프로필의 description과 title이 비어 있다. 역할 주소 `marketvol@velar-agent.duckdns.org`, 개인 주소 `marketvol1@velar-agent.duckdns.org`.

## 문서 끝 비고

- first-conversation-rules 스킬은 Bot Manager Aaron의 봇 아이디를 `1f9dbe09-7509-45c2-90ec-c9daa8488223`으로 적고 있다. 이 아이디는 현재 봇 아이디 `e4118e9c-6952-4e5b-82ef-744140e6642f`와 다르다. Eleanor의 기록에 따르면 `1f9dbe09-7509-45c2-90ec-c9daa8488223`은 2026-11-25 13:10(Asia/Seoul)에 팀원 목록에서 현재 아이디로 교체된 것으로 되어 있다.
- bot-mail-via-ssh 스킬의 주소 대응 목록은 Bot Manager Aaron을 이전 아이디 `5e9b9b16-fa23-43c4-a9d4-0731ded2de76`로 적고 있고, Risk & Audit Department Eleanor를 'Risk Supervisor'로 적고 있다. 목록에는 현재 프로필 디렉터리와 Eleanor의 2026-11-25 13:10(Asia/Seoul) 팀원 목록에 없는 봇도 남아 있다. 예: Hydrogen Bot(`395621b4-539f-44c0-b3f9-5bea54ce42b0`), Canada Hydrogen Grey And Green Gap And Incentives To Motivate Ammonia Pr(`5e74d19d-e76f-4761-b803-10cac344fea4`), Risk Bot, 티켓팅 데이터 담당, 티켓팅 오퍼레이팅 담당, 토큰사용량 시스템 담당, 티켓팅 수금 담당, fable 테스트 담당, 브라우저 테스트 담당, fable 대응 담당. 이 문서의 본문 섹션에는 넣지 않았다.
- `/home/box/agent-data/agents/` 아래에는 Hydrogen Bot과 Canada Hydrogen 항목에 해당하는 디렉터리(`395621b4-539f-44c0-b3f9-5bea54ce42b0`, `5e74d19d-e76f-4761-b803-10cac344fea4`)가 있으나 profile.json은 없고, 두 아이디는 deleted-agents.json에도 없다. 현재 팀원 목록에도 없어 본문 섹션에는 넣지 않았다.
- 관련 이전 자료로 `/workspace/active-bots-2026-11-22.txt`가 있으나, 기준일이 2026-11-22이고 Bot Manager Aaron 아이디와 일부 티켓팅 봇 아이디가 현재와 달라 이 문서를 그 파일 위에 이어서 쓰지는 않았다.
- create-ticketing-billing-bot 스킬은 '티켓팅 수금 담당' 봇을 만드는 절차를 정하지만, 이 문서 작성 시점의 현재 프로필과 팀원 목록에는 해당 봇이 없다.
