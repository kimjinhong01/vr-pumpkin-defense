# Unity VR 디펜스 슈팅 게임

![VR Shooter](https://img.youtube.com/vi/MuP1mdIqHVw/maxresdefault.jpg)

[**시연 영상 보기**](https://youtu.be/MuP1mdIqHVw)

---

## 프로젝트 개요

Unity와 XR Interaction Toolkit 기반으로 제작된 **VR 디펜스 슈팅 게임**입니다.
플레이어는 VR 컨트롤러를 활용해 무기를 조작하며, 본진(Core)을 향해 몰려오는 적들을 방어하는 것이 목적입니다.
**웨이브 시스템, VR 무기 조작, 시선 기반 인터랙션** 등 다양한 VR 인터페이스가 구현되어 있습니다.

---

## 주요 기능

| 시스템         | 설명                                                          |
| ----------- | ----------------------------------------------------------- |
| 총기 시스템      | VR에서 무기를 잡고, 방아쇠로 발사, 리로드 가능 (`Gun`, `Shooter`, `Magazine`) |
| 적 웨이브 시스템   | 시간이 지날수록 점점 더 많은 적이 등장 (`Spawner`, `MobManager`)            |
| 본진(Core) 방어 | Core 도달 시 체력 감소 → 0이면 게임오버                                  |
| 피격 및 효과     | 총에 맞은 적은 VFX, SFX, 진동 등 즉각적인 피드백 제공                         |
| 조준 시스템      | 레이저 및 표적 시각화 (`RayVisualizer`, `Reticle`)                   |
| UI          | 실시간 생존 시간, 남은 적 수, 탄약, 본진 체력 표시                             |
| VR 인터랙션     | 시선 기반 활성화, 무기 자동 리로드, 햅틱 피드백 등 지원                           |

---

## 게임 플레이 흐름

```
Start → Spawner 활성화 → 적 웨이브 시작 → 전투 진행
→ 적 본진 도달 시 Core HP 감소 → HP 0이면 GameOver
→ 플레이어가 생존하면 계속 다음 웨이브 생성
```

---

## 코드 및 폴더 구조

```bash
Assets/
├── Scripts/
│   ├── Weapon/
│   │   ├── Gun.cs                 # 무기 잡기/놓기 이벤트
│   │   ├── Shooter.cs             # 발사 로직 (레이캐스트 기반)
│   │   ├── Magazine.cs            # 탄약 저장 및 리로드 처리
│   │   └── WeaponStand.cs         # 무기 스탠드 및 자동 리로드
│   ├── Enemy/
│   │   ├── Mob.cs                 # 적 유닛 로직 (이동/피격/도달 처리)
│   │   ├── MobManager.cs          # 적 전체 관리 및 일괄 제거
│   │   └── Spawner.cs             # 적 스폰 웨이브 로직
│   ├── Core/
│   │   ├── Core.cs                # 본진 체력, GameOver 처리
│   │   └── ChangeAgentDestinationToCore.cs
│   ├── Interaction/
│   │   ├── ActivateOnLookAt.cs   # 시선 기반 상호작용
│   │   ├── PlayHapticOnInteractable.cs
│   │   ├── FlashLight.cs, FlashLineRenderer.cs, FlashVolume.cs
│   ├── Visual/
│   │   └── RayVisualizer.cs       # 레이저 시각화
│   ├── UI/
│   │   ├── MobCounterUI.cs
│   │   ├── SurvivalTimeUI.cs
│   │   └── OnHpChanged.cs
```

---

## 조작 방법 (VR 컨트롤러 기준)

| 기능       | 조작 방식               |
| -------- | ------------------- |
| 이동       | 정지형 또는 텔레포트 기반 이동   |
| 무기 집기/놓기 | 컨트롤러 트리거로 Grab      |
| 발사       | 트리거 버튼              |
| 리로드      | 탄창 근처 무기 스탠드에 장착    |
| 조준       | 손의 방향 + 레이저 시각화     |
| 텔레포트     | 커서 조준 후 버튼 클릭       |
| UI 확인    | HUD 또는 월드 공간 UI를 통해 |

※ `XR Rig`에 따라 조작법이 달라질 수 있음

---

## 실행 방법

1. Unity 2021 이상에서 프로젝트 열기
2. **XR Interaction Toolkit 세팅 필수**
3. `Scene` 열기 → `Spawner`, `Core`, `XR Rig` 확인
4. ▶ 버튼 클릭 후 VR 디바이스에서 게임 실행

---

## 웨이브 시스템 요약

* **`Spawner`**: 시간에 따라 `Mob` 다수 소환
* **`Mob.cs`**: `NavMeshAgent` 기반으로 Core를 향해 이동
* **`MobManager.cs`**: 적 유닛 일괄 관리 및 리셋
* **Core.cs**: 적 도달 시 체력 감소 및 게임오버 판단

---

## 향후 개선 사항

* 스테이지별 보스 추가 (패턴/체력바 포함)
* 무기 종류 추가 (샷건, 레이저 등)
* Co-op 플레이 도입 (멀티플레이 VR)
* 난이도 모드 및 웨이브 속도 조절 옵션
* 피격 시 화면 블러/HitStop 등 연출 강화
* 무기 이펙트/피격 VFX 커스터마이징 시스템

---

## 라이선스

```
MIT License

본 프로젝트는 자유롭게 사용/수정/배포 가능하며, 상업적 사용 시 출처 표기를 권장합니다.
```

---

## 시연 영상 다시 보기

[![Demo Video](https://img.youtube.com/vi/MuP1mdIqHVw/0.jpg)](https://youtu.be/MuP1mdIqHVw)

[https://youtu.be/MuP1mdIqHVw](https://youtu.be/MuP1mdIqHVw)
