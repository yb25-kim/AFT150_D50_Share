# AFT150-D50 샘플 프로그램 (Linux)

AIDIN ROBOTICS 6축 힘/토크 센서 **AFT150-D50** 을 리눅스에서 사용하기 위한 프로그램입니다.

그림이 포함된 상세 안내는 **[guide.html](guide.html)** 을 내려받아 브라우저로 여세요.

---

## 1. 내려받기 — Jetson (v1.1.0)

| 장비 | 내려받을 파일 |
|---|---|
| Jetson (aarch64) | `aft150-d50-sample-program-linux-v1.1.0-bin-aarch64.tar.gz` |

> **JetPack 6 (Ubuntu 22.04)** 에서 확인했습니다.
> 장비 확인: `uname -m` 결과가 `aarch64` 인지 확인하세요.

## 2. 설치

```bash
tar xzf aft150-d50-sample-program-linux-v1.1.0-bin-aarch64.tar.gz
cd aft150-d50-sample-program-linux-v1.1.0-bin-aarch64

sudo ./install.sh
```

CAN 어댑터 드라이버, 자동 기동 설정, 메뉴 아이콘까지 한 번에 설치됩니다.
설치에는 **인터넷 연결과 sudo 권한**이 필요합니다.

설치가 끝나면 **한 번 로그아웃했다 다시 로그인**하세요.
CANable 사용에 필요한 권한이 그때 적용됩니다.

## 3. 실행

```bash
./run.sh
```

메뉴의 **AFT150-D50 샘플 프로그램** 아이콘으로도 실행됩니다.

## 4. 센서 2개 동시 사용

센서마다 CAN 어댑터를 하나씩 연결하고, 어댑터에 고정 이름을 붙인 뒤 창을 하나씩 띄웁니다.

```bash
sudo scripts/name-adapters.sh     # 연결된 어댑터에 aft150-a, aft150-b 이름 붙이기 (처음 한 번)
./run.sh aft150-a                 # 센서 1
./run.sh aft150-b                 # 센서 2 (다른 터미널에서)
```

- 어느 어댑터가 어느 센서인지 모르겠으면 하나만 꽂고 `scripts/name-adapters.sh --list` 로 확인하세요.
- PCAN 은 이름을 붙인 뒤 USB 를 한 번 다시 꽂아야 적용되며, 같은 USB 포트에 꽂아야 같은 이름이 됩니다.

## 5. 사용 순서

```
① 어댑터 선택 → [연결]          (./run.sh aft150-a 로 실행하면 자동 연결)
② CAN 모드 선택 → [① MODE]
③ 데이터 타입·레이트 선택 → [② TRANSMIT]
```

> **[① MODE] 만 누르면 데이터가 나오지 않습니다.**
> 센서가 모드 변경 시 송신을 멈추기 때문이며, 고장이 아닙니다.
> 반드시 **[② TRANSMIT]** 을 눌러야 송신이 재개됩니다.

---

## 지원 어댑터

| 어댑터 | 지원 |
|---|---|
| PEAK PCAN-USB FD | CAN FD (1M/4M) / CAN 2.0 |
| PEAK PCAN-USB | CAN 2.0 |
| CANable 2.0 (AIDIN 펌웨어) | CAN FD (1M/4M) / CAN 2.0 |
| CANable 2.0 (순정 펌웨어) | CAN 2.0 |

USB 어댑터는 꽂기만 하면 준비됩니다 (재부팅 후에도).

### CANable 로 CAN FD 를 쓰려면 — 펌웨어 굽기 (어댑터마다 한 번)

```bash
sudo scripts/canable-fw/flash-canable.sh
# "기다립니다" 가 나오면 CANable 의 BOOT 두 핀(120R 옆, 보드 표기 BOOT)에 점퍼 캡을 꽂고 USB 연결
# 끝나면 점퍼 캡을 빼고 USB 를 다시 꽂는다
```

> 굽기가 끝나면 **BOOT 점퍼 캡을 반드시 빼 주세요.** 꽂혀 있으면 CAN 통신이 되지 않습니다.

## 문제가 생기면

```bash
./run.sh --check
```

설치 상태와 어댑터 인식을 한 번에 점검합니다.

| 증상 | 확인할 것 |
|---|---|
| 어댑터 목록이 비어 있다 | USB 를 다시 꽂고 화면의 `새로고침` |
| CANable 만 안 잡힌다 | 로그아웃 후 다시 로그인했는지 확인 |
| CANable 로 CAN FD 데이터가 안 나온다 | CANable 펌웨어를 굽고, BOOT 점퍼 캡을 뺐는지 확인 |

## 제거

```bash
sudo ./install.sh --uninstall
```

---

## 이전 버전 (v1.0.1)

`aft150-d50-sample-program-linux-v1.0.1-bin-x86_64.tar.gz` / `...-v1.0.1-bin-aarch64.tar.gz`

---

제3자 소프트웨어 라이선스는 배포본에 포함된 `THIRD-PARTY-NOTICES.md` 를 참조하세요.

© AIDIN ROBOTICS
