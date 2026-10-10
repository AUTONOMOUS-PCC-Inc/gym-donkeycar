<div align="center">

### 업스트림 포크의 최신 커밋이 모든 파일을 지웠다. 그래서 복제해 왔다.

AUTONOMOUS PCC의 자율주행 교육 과정이 서브모듈로 **고정(pin)** 해 쓰는<br>
[tawnkramer/gym-donkeycar](https://github.com/tawnkramer/gym-donkeycar) 미러입니다. 이 README 한 장을 제외하고 코드는 손대지 않았습니다.

![Mirror](https://img.shields.io/badge/저장소-Mirror-6B7280?style=for-the-badge)
![Upstream](https://img.shields.io/badge/Upstream-tawnkramer%2Fgym--donkeycar-0B1B33?style=for-the-badge)
![Version](https://img.shields.io/badge/gym--donkeycar-1.3.1-1E6FD9?style=for-the-badge)
![Envs](https://img.shields.io/badge/트랙-11종-1E6FD9?style=for-the-badge)
![Pinned](https://img.shields.io/badge/고정커밋-beac6ff-16A34A?style=for-the-badge)
![Default](https://img.shields.io/badge/기본브랜치-aypi--pinned-7C3AED?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-A3A3A3?style=for-the-badge)

[**⚠ 먼저 읽을 것**](#-master-브랜치는-파일이-0개다) · [**왜 있나**](#왜-이-저장소가-있나) · [**출처**](#출처) · [**어떻게 쓰이나**](#어떻게-쓰이나) · [**하지 말 것**](#하지-말-것) · [**라이선스**](#라이선스)

<br>

```
tawnkramer/gym-donkeycar           원본 (upstream)
        │  fork
        ▼
YUNSUNGWOONG/gym-donkeycar         강사 개인 포크
        │                            master 끝점 0a805ad → 파일 전부 삭제  ⚠
        │  git push --mirror  ·  2026-10-10
        ▼
AUTONOMOUS-PCC-Inc/gym-donkeycar   ← 이 저장소 · 기본 브랜치 aypi-pinned
        │  서브모듈로 SHA 고정
        ▼
aypi-car-tutorial                  바이브코딩 캠프 실습 저장소
```

<sub>전체 이력 <strong>249 커밋</strong>을 그대로 복제했습니다. 고정 커밋 기준 파일 60개, 변경 없음.</sub>

</div>

---

## ⚠ `master` 브랜치는 파일이 0개다

복제 과정에서 발견한 사실입니다. 포크의 `master` 최신 커밋이 저장소의 **모든 파일을 삭제**했습니다.

| | 내용 |
|---|---|
| 커밋 | `0a805ad20e3cc3acb5a076b194455ed54219c8dc` (2024-02-16, 메시지 `d`) |
| 트리 | `4b825dc642cb6eb9a060e54bf8d69288fbee4904` — git의 **빈 트리** SHA |
| 결과 | 그 브랜치를 체크아웃하면 `gym_donkeycar/` 도 `setup.py` 도 `LICENSE` 도 없습니다 |

교육 과정이 지금까지 멀쩡했던 이유는 단 하나입니다. 실습 저장소가 그 **직전** 커밋
`beac6ff`(파일 60개)를 SHA로 고정해 두고 있어서, 브랜치 끝점을 쳐다보지 않기 때문입니다.

> 이 미러의 **기본 브랜치를 `aypi-pinned`(= `beac6ff`)로 설정**한 이유가 이것입니다.
> `master`를 기본값으로 두면 저장소를 열었을 때 코드도 라이선스도 보이지 않습니다.
> `master`는 이력 보존을 위해 삭제하지 않고 그대로 남겨 두었습니다.

---

## 왜 이 저장소가 있나

교육용 실습 저장소가 **강사 개인 계정의 포크**를 서브모듈로 가리키고 있었습니다.

| 항목 | 내용 |
|---|---|
| **끊기면 수업이 멈춘다** | 개인 계정의 저장소 이름이 바뀌거나 비공개로 전환되면, 학생의 `git clone --recurse-submodules`가 그 자리에서 실패합니다. |
| **개인 포크의 브랜치는 움직인다** | 위에 적은 대로, 실제로 끝점이 빈 트리가 되었습니다. 교육 자료가 의존하는 브랜치에서 일어난 일입니다. |
| **조직이 책임지는 사본이 필요하다** | 교육 과정은 회사 산출물입니다. 그 의존성도 조직 계정에 있어야 보존·접근 권한을 회사가 관리할 수 있습니다. |

> 그래서 코드를 바꾸지 않고 **이력 전체를 조직 계정으로 복제**했습니다.
> 업스트림을 대체하려는 것이 아니라, **교육 과정이 붙잡고 있을 고정점**을 만들기 위한 사본입니다.

---

## 출처

| 단계 | 저장소 | 비고 |
|---|---|---|
| 원본 | [`tawnkramer/gym-donkeycar`](https://github.com/tawnkramer/gym-donkeycar) | OpenAI Gym 환경 본체 (MIT) |
| 포크 | [`YUNSUNGWOONG/gym-donkeycar`](https://github.com/YUNSUNGWOONG/gym-donkeycar) | 강사 개인 포크 · `master` 끝점 비어 있음 |
| 미러 | `AUTONOMOUS-PCC-Inc/gym-donkeycar` | 이 저장소 · 2026-10-10 `git push --mirror` |

미러 푸시로 만들었기 때문에 GitHub에 **포크 배지가 표시되지 않습니다.** 이 문서가 그 출처 표기입니다.

**고정 커밋 `beac6ff46f6ec9f61798be28dcaec4bb598a2602`** (2023-09-08, `fixing CI (#82)`)은
업스트림 `tawnkramer/gym-donkeycar`에 **같은 SHA로 존재하는 커밋**입니다.
즉 교육 과정이 쓰는 코드는 개인 포크에서 수정된 것이 아니라 업스트림 원본 트리입니다.

> 이 README 커밋의 **부모가 바로 그 고정 커밋**입니다.
> `aypi-pinned`의 끝점은 README가 올라가며 한 커밋 앞으로 움직였지만, 서브모듈이 가리키는 SHA는 그대로입니다.

---

## 어떻게 쓰이나

**AUTONOMOUS PCC 바이브코딩 캠프 1회차(자율주행)** 에서 Unity 시뮬레이터와 donkeycar를 잇는 계층입니다.
학생의 `myconfig.py`가 `DONKEY_GYM = True`로 켜면 donkeycar가 이 패키지를 통해
TCP 9091로 시뮬레이터에 붙고, 학생은 웹 UI에서 차를 운전해 주행 데이터를 모읍니다.

```python
# cars/mycar/myconfig.py
DONKEY_GYM = True
DONKEY_SIM_PATH = "../../DonkeySimWin/donkey_sim.exe"
DONKEY_GYM_ENV_NAME = "donkey-generated-track-v0"
```

등록된 트랙은 11종입니다 — `donkey-generated-track-v0`, `donkey-generated-roads-v0`,
`donkey-warehouse-v0`, `donkey-avc-sparkfun-v0`, `donkey-mountain-track-v0`,
`donkey-roboracingleague-track-v0`, `donkey-waveshare-v0`, `donkey-minimonaco-track-v0` 등.

의존성은 `gym==0.22`, `numpy`, `pillow`이고 `python_requires>=3.7`입니다.
교육 과정은 Python 3.9 conda 환경에서 돌립니다.

> **시뮬레이터 첫 실행 시 `Could not connect to server. Is it running?`** — 기본
> `start_delay`가 5초인데 exe의 콜드 스타트가 그보다 오래 걸려서입니다. `GYM_CONF`에
> `start_delay`를 15로 올리면 해결됩니다 (2026-10-10 리허설에서 확인).

이 저장소를 단독으로 쓸 일은 없습니다. 설치 순서·conda 환경·시뮬레이터 설정은 실습 저장소의 안내서를 따르세요.

> 실습 저장소 `aypi-car-tutorial`은 준비 중이며, 현재 고정 주체는 [`YUNSUNGWOONG/DonkeyBro`](https://github.com/YUNSUNGWOONG/DonkeyBro)입니다.

---

## 하지 말 것

- **`git submodule update --remote`를 절대 쓰지 마세요.** `.gitmodules`에 `branch = master`가 적혀 있어서, 이 명령은 고정된 SHA를 버리고 **파일이 0개인 끝점**을 체크아웃합니다. 서브모듈 폴더가 비워집니다. 교육 과정에서는 항상 아래를 씁니다.

```bash
git submodule update --init --recursive   # 고정된 SHA를 체크아웃 (안전)
```

- **`master` 브랜치를 기본값으로 되돌리지 마세요.** 위의 ⚠ 절을 보세요.
- **이 저장소에 이슈·PR을 올리지 마세요.** 코드 문제는 업스트림 [tawnkramer/gym-donkeycar](https://github.com/tawnkramer/gym-donkeycar/issues)로 가야 합니다. 여기는 사본입니다.

---

## 원본 문서

업스트림 README는 **고정 커밋 시점 그대로** 아래에 남아 있습니다.

- [README.md @ `beac6ff`](https://github.com/AUTONOMOUS-PCC-Inc/gym-donkeycar/blob/beac6ff46f6ec9f61798be28dcaec4bb598a2602/README.md)
- 시뮬레이터 빌드 배포 · [tawnkramer/gym-donkeycar releases](https://github.com/tawnkramer/gym-donkeycar/releases)

---

## 라이선스

**MIT License**입니다. 원 저작권 표기를 그대로 보존했습니다.

```
MIT License

Original Work Copyright (c) 2018 Tawn Kramer
Original Work Copyright (c) 2018 Roma Sokolkov
Modified Work Copyright (c) 2019, Leigh Johnson
```

전문은 [`LICENSE`](LICENSE)를 보세요. 이 미러는 저작권자를 바꾸지 않으며, 재배포 사본으로서 원 고지를 유지합니다.

---

<div align="center">
<sub><strong>AUTONOMOUS PCC, Inc.</strong> · (주)오토노머스피씨씨 — 교육 과정 의존성 미러</sub><br>
<sub>조직 소개 · <a href="https://github.com/AUTONOMOUS-PCC-Inc">github.com/AUTONOMOUS-PCC-Inc</a></sub>
</div>
