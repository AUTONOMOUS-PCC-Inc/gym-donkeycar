<div align="center">

<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/gym-banner.svg" alt="gym-donkeycar — donkeycar 주행 루프와 Unity 시뮬레이터를 TCP 9091로 잇는 다리" width="100%">

### 네 코드와 시뮬레이터 사이를 잇는 다리.

실습 저장소를 클론할 때 **같이 따라온 폴더**입니다. 따로 내려받을 필요 없습니다.<br>
여기는 설치할 것도 없습니다 — donkeycar가 알아서 불러다 씁니다.

![Version](https://img.shields.io/badge/gym--donkeycar-1.3.1-1E6FD9?style=for-the-badge)
![Tracks](https://img.shields.io/badge/트랙-11종-1E6FD9?style=for-the-badge)
![Port](https://img.shields.io/badge/TCP-9091-16A34A?style=for-the-badge)
![WebUI](https://img.shields.io/badge/웹UI-8887-16A34A?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-A3A3A3?style=for-the-badge)

[**무슨 일을 하나**](#무슨-일을-하나) · [**설정**](#myconfigpy-에서-켠다) · [**안 될 때**](#잘-안-될-때) · [**폴더가 비었다면**](#폴더가-비어-있다면) · [**출처**](#이-저장소에-대해)

</div>

---

## 무슨 일을 하나

네가 `python manage.py drive` 를 치면, donkeycar는 진짜 RC카 대신 **Unity 시뮬레이터**를
차로 씁니다. 그 사이를 이어 주는 게 이 폴더입니다.

<div align="center">
<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/gym-dataflow.svg" alt="데이터 흐름: myconfig.py → donkeycar 주행 루프 → 이 저장소 → TCP 9091 → Unity 시뮬레이터. 사람은 브라우저 8887에서 운전한다" width="100%">
</div>

순서대로 읽으면 이렇습니다.

1. `myconfig.py` 에서 "시뮬레이터를 쓰겠다"고 켠다
2. donkeycar가 주행 루프를 돈다
3. **이 폴더**가 시뮬레이터 실행 파일을 띄우고 소켓(9091)으로 붙는다
4. 시뮬레이터가 160x120 카메라 사진을 보내 주고, 조향 명령을 받아 차를 움직인다
5. 너는 브라우저 `localhost:8887` 에서 운전한다

즉 **네가 보는 화면 두 개**(시뮬레이터 창과 브라우저)가 이 다리로 연결돼 있습니다.

---

## `myconfig.py` 에서 켠다

`cars/mycar/myconfig.py` 에 아래를 넣습니다. 이 파일만 건드리면 되고, 이 폴더 안의
코드는 손댈 일이 없습니다.

```python
DONKEY_GYM = True
DONKEY_SIM_PATH = "../../DonkeySimWin/donkey_sim.exe"
DONKEY_GYM_ENV_NAME = "donkey-generated-track-v0"
```

트랙은 11종이 등록돼 있습니다. `DONKEY_GYM_ENV_NAME` 을 바꾸면 다른 코스로 갑니다.

```
donkey-generated-track-v0        donkey-generated-roads-v0
donkey-warehouse-v0              donkey-avc-sparkfun-v0
donkey-mountain-track-v0         donkey-roboracingleague-track-v0
donkey-waveshare-v0              donkey-minimonaco-track-v0
```

> 수업은 `donkey-generated-track-v0` 로 진행합니다. 다른 트랙은 다 끝낸 뒤에 바꿔 보세요.
> 트랙을 바꾸면 **그 트랙에서 모은 데이터로 다시 학습해야** 합니다 — 모델은 자기가 본
> 길만 압니다.

---

## 잘 안 될 때

| 증상 | 원인과 해결 |
|---|---|
| `Could not connect to server. Is it running?` | **첫 실행이면 거의 다 이겁니다.** 시뮬레이터가 켜지는 데 걸리는 시간보다 기다려 주는 시간(기본 5초)이 짧아서 생깁니다. `myconfig.py` 의 `GYM_CONF` 에 `start_delay` 를 **15**로 올리면 해결됩니다. 안내서에 적힌 대로 넣으세요. |
| 시뮬레이터 창은 떴는데 브라우저가 안 열린다 | 주소를 직접 치세요 — `localhost:8887`. 자동으로 안 열리는 경우가 있습니다. |
| 시뮬레이터 창이 아예 안 뜬다 | `DONKEY_SIM_PATH` 경로가 틀렸습니다. `donkey_sim.exe` 가 실제로 그 자리에 있는지 확인하세요. 경로는 `cars/mycar` 기준 상대경로입니다. |
| 차가 제자리에서 덜덜 떨거나 안 움직인다 | 브라우저 화면을 한 번 클릭해 포커스를 준 뒤 조작하세요. 그래도 안 되면 시뮬레이터와 `manage.py` 를 둘 다 끄고 다시 시작하세요. |
| 이 폴더가 텅 비어 있다 | 아래 [폴더가 비어 있다면](#폴더가-비어-있다면)을 보세요. |

그래도 안 되면 **에러 메시지 전체를 복사해서** 강사에게 보여 주세요.

---

## 폴더가 비어 있다면

서브모듈을 안 받았거나, **최신으로 끌어오는 명령을 썼기** 때문입니다.
실습 저장소 맨 위에서 아래를 실행하면 돌아옵니다.

```bash
git submodule update --init --recursive
```

이 명령을 쓰는 이유가 있습니다. 이 저장소의 `master` 브랜치는 **파일이 0개**입니다.
과거 어느 시점에 전부 삭제된 커밋이 올라갔고, 수업은 그 **직전** 버전을 콕 집어
쓰고 있습니다. 그래서 "최신으로 끌어오는" 명령을 쓰면 폴더가 비워집니다.

<div align="center">
<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/gym-branches.svg" alt="브랜치 구조: aypi-pinned는 파일 60개, master 끝점은 빈 트리로 파일 0개. --init --recursive는 안전하고 --remote는 폴더를 비운다" width="100%">
</div>

> **`git submodule update --remote` 는 절대 쓰지 마세요.** 위 그림의 빨간 쪽으로 갑니다.
> 그리고 이 저장소의 기본 브랜치가 `master` 가 아니라 `aypi-pinned` 인 것도 같은 이유입니다.

---

## 이 저장소에 대해

[tawnkramer/gym-donkeycar](https://github.com/tawnkramer/gym-donkeycar)를 **그대로
복제한 사본**입니다. 수업이 개인 계정에 의존하지 않도록 회사 조직 계정에 두었습니다.
이 README 한 장 말고는 코드를 손대지 않았고, 수업이 쓰는 커밋은 원본에 **같은 SHA로
존재하는** 커밋이라 네가 쓰는 건 원본 코드 그대로입니다.

<div align="center">
<img src="https://raw.githubusercontent.com/AUTONOMOUS-PCC-Inc/.github/main/mirrors/assets/gym-provenance.svg" alt="출처 사슬: tawnkramer 원본 → master 끝점이 빈 개인 포크 → AUTONOMOUS PCC 미러 → 실습 저장소" width="100%">
</div>

| 단계 | 저장소 |
|---|---|
| 원본 | [`tawnkramer/gym-donkeycar`](https://github.com/tawnkramer/gym-donkeycar) |
| 포크 | [`YUNSUNGWOONG/gym-donkeycar`](https://github.com/YUNSUNGWOONG/gym-donkeycar) |
| 사본 | `AUTONOMOUS-PCC-Inc/gym-donkeycar` · 2026-10-10 `git push --mirror` |

고정 커밋은 `beac6ff46f6ec9f61798be28dcaec4bb598a2602` (2023-09-08)입니다.
미러 푸시라 GitHub에 포크 배지가 안 붙으므로, 이 절이 출처 표기입니다.
라이브러리 자체의 문제는 여기가 아니라 원본
[tawnkramer/gym-donkeycar](https://github.com/tawnkramer/gym-donkeycar/issues)로 가야 합니다.

**원본 README**는 그 커밋 시점 그대로
[여기](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar/blob/beac6ff46f6ec9f61798be28dcaec4bb598a2602/README.md)에
남아 있습니다. 시뮬레이터 실행 파일은 이 저장소에 없고
[원본 릴리스 페이지](https://github.com/tawnkramer/gym-donkeycar/releases)에서 받습니다.

### 라이선스

**MIT License**이고 원 저작권 표기를 그대로 보존했습니다.

```
MIT License

Original Work Copyright (c) 2018 Tawn Kramer
Original Work Copyright (c) 2018 Roma Sokolkov
Modified Work Copyright (c) 2019, Leigh Johnson
```

전문은 [`LICENSE`](LICENSE)에 있습니다.

---

<div align="center">
<sub><strong>AUTONOMOUS PCC, Inc.</strong> · (주)오토노머스피씨씨 — 바이브코딩 캠프 1회차 실습용</sub><br>
<sub><a href="https://github.com/AUTONOMOUS-PCC-Inc">github.com/AUTONOMOUS-PCC-Inc</a></sub>
</div>
