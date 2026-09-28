# AFT150-D50 샘플 프로그램 (Linux)

AIDIN ROBOTICS 6축 힘/토크 센서 **AFT150-D50** 을 리눅스 PC 에서 사용하기 위한 프로그램입니다.

그림이 포함된 상세 안내는 **[guide.html](guide.html)** 을 내려받아 브라우저로 여세요.

---

## 1. 내려받기

장비에서 아래 명령으로 아키텍처를 확인하고, 맞는 파일을 받으세요.

```bash
uname -m
```

| 결과 | 장비 | 내려받을 파일 |
|---|---|---|
| `x86_64` | 일반 PC | `aft150-d50-sample-program-linux-v1.0.1-bin-x86_64.tar.gz` |
| `aarch64` | Jetson 등 | `aft150-d50-sample-program-linux-v1.0.1-bin-aarch64.tar.gz` |

> **Ubuntu 22.04 이상**이 필요합니다.

## 2. 설치

```bash
tar xzf aft150-d50-sample-program-linux-v1.0.1-bin-x86_64.tar.gz
cd aft150-d50-sample-program-linux-v1.0.1-bin-x86_64

sudo ./install.sh
```

CAN 어댑터 드라이버, 자동 기동 설정, 메뉴 아이콘까지 한 번에 설치됩니다.
설치에는 **인터넷 연결과 sudo 권한**이 필요합니다.

설치가 끝나면 **한 번 로그아웃했다 다시 로그인**하세요.
시리얼 어댑터(CANable) 사용에 필요한 권한이 그때 적용됩니다.

## 3. 실행

```bash
./run.sh
```

메뉴의 **AFT150-D50 샘플 프로그램** 아이콘으로도 실행됩니다.

## 4. 사용 순서

```
① 어댑터 선택 → [연결]
② CAN 모드 선택 → [① MODE]
③ 데이터 타입·레이트 선택 → [② TRANSMIT]
```

> **[① MODE] 만 누르면 데이터가 나오지 않습니다.**
> 센서가 모드 변경 시 송신을 멈추기 때문이며, 고장이 아닙니다.
> 반드시 **[② TRANSMIT]** 을 눌러야 송신이 재개됩니다.

---

## 지원 어댑터

| 어댑터 | 비고 |
|---|---|
| PEAK PCAN-USB / FD | CAN FD + BRS 지원 |
| IXXAT USB-to-CAN (FD) | CAN FD + BRS 지원 |
| CANable (slcan 펌웨어) | 클래식 CAN 2.0 전용 |

USB 어댑터는 꽂기만 하면 준비됩니다 (재부팅 후에도).

## 문제가 생기면

```bash
./run.sh --check
```

설치 상태와 어댑터 인식을 한 번에 점검합니다.

| 증상 | 확인할 것 |
|---|---|
| 어댑터 목록이 비어 있다 | USB 를 다시 꽂고 화면의 `새로고침` |
| CANable 만 안 잡힌다 | 로그아웃 후 다시 로그인했는지 확인 |
| IXXAT 가 안 잡힌다 | `sudo ./install.sh` 재실행 (커널 업데이트 직후 필요) |

## 제거

```bash
sudo ./install.sh --uninstall
```

---

제3자 소프트웨어 라이선스는 배포본에 포함된 `THIRD-PARTY-NOTICES.md` 를 참조하세요.

© AIDIN ROBOTICS
