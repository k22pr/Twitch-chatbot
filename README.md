# Twitch-ChatBot

트위치 챗봇입니다. TypeScript 로 제작 되었습니다.

별도의 관리 페이지가 아닌 채팅창에서 명령어를 통해 관리 하실 수 있습니다.

## 목차

1. [구조](#구조)
2. [고정 명령어](#고정_명령어)
   1. [고정 명령어 예제](#고정_명령어_예제)
3. [초기 명령어](#초기_명령어)

## 구조

챗봇의 구조입니다.

- ChatBot(main)
  - Channel : Channel[] (채널 클레스)
    - name : string (채널의 이름)
    - Commander : Commander (명령어 집합)
      - commands : array (해당 채널의 명령어 목록)
        - command : string (반응 할 문자열)
        - respone : string (응답 할 문자열)
        - admin : boolean (관리자 명령어 여부)
        - static : boolean (고정명령어 여부)
  - ChatData : 채팅 데이터

## 고정 명령어

봇에서 정의되어있는 명령어 입니다.

해당하는 명령어는 삭제하실 수 없으며 다른 명령어로 덮어씌우실 수 없습니다.

| 명령어                              | 응답 | 관리자여부 | 설명                                            |
| ----------------------------------- | ---- | ---------- | ----------------------------------------------- |
| !추가 (추가할 명령어) (응답할 반응) | x    | yes        | 새로 응답할 명령어를 추가합니다.                |
| !삭제 (삭제할 명령어)               | x    | yes        | 저장되어있는 **(삭제할 명령어)** 를 삭제합니다. |
| ! 초기화                            | x    | yes        | 설정된 모든 명령어를 초기상태로 되돌립니다.     |
| ! 벤 (사용자 아이디)                | x    | yes        | **(사용자 아이디)** 를 체널에서 벤시킵니다.     |
| ! 언벤 (사용자 아이디)              | x    | yes        | **(사용자 아이디)** 의 벤상태를 해제합니다.     |

## 고정 명령어 예제

#### !추가 {명령어} {응답}

새로운 명령어를 추가합니다. **!{명령어}** 를 사용자가 입력했을때 **{응답}** 으로 자동응답 합니다.

만약 기존에 존재하던 명령어를 입력하실 경우 새로 입력하신 응답으로 덮어씌워집니다.

```
    !추가 맴버 섭봇, 서버지기
    >> !맴버 명령어가 추가되었습니다.

    !맴버
    >> 섭봇, 서버지기

    !추가 맴버 섭봇
    >> !맴버 명령어가 추가되었습니다.

    !맴버
    >> 섭봇
```

### !삭제 {명령어}

**{명령어}** 에 해당하는 명령어를 삭제합니다.

고정 명령의경우 삭제하실 수 없습니다.

```
    !삭제 맴버
    >> !맴버 명령어가 삭제되었습니다.

    !맴버
    >>
```

### !초기화

지정한 모든 명령어를 삭제하고 초기상태로 되돌립니다.

```
    !초기화
    >> 사용자 지정 명령어가 모두 삭제되었습니다.
```

### !벤 {닉네임} {사유}(optional)

**{닉네임}** 에 해당하는 사용자를 채널에서 영구적으로 쫒아냅니다.

**{사유}(optional)** 는 필수가 아니며 입력하실 경우 벤사유를 입력하실 수 있습니다.

```
    !벤 test 도배
    chatBot님이 test님을 강제 퇴장시켰습니다. 이유: 도배
```

### !언벤 {닉네임}

**{닉네임}** 에 해당하는 사용자의 벤 상태를 해제합니다.

```
    !언벤 test
    chatBot님이 test님의 강제 퇴장을 해제했습니다.
```

## 초기 명령어

기본적으로 제공되는 명령어 입니다.

원치않는 명령어는 !삭제 를 통해 삭제하실 수 있습니다.

!초기화시 다시 기본적으로 생성됩니다.

| 명령어  | 응답     | 관리자여부 | 설명                                                |
| ------- | -------- | ---------- | --------------------------------------------------- |
| !업타임 | {UPTIME} | no         | 방송을 시작한 시간을 알려줍니다.                    |
| !게임   | {GAME}   | no         | 현재 Twitch 에 설정된 플레이중인 게임을 알려줍니다. |
| !방제   | {TITLE}  | no         | 현재 설정된 방의 제목을 알려줍니다.                 |
