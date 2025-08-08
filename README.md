# VR 디펜스 슈팅 게임 – Unity 프로젝트

![YouTube Thumbnail](https://img.youtube.com/vi/MuP1mdIqHVw/maxresdefault.jpg)
[시연 영상 바로가기](https://youtu.be/MuP1mdIqHVw)

---

## 프로젝트 개요

이 프로젝트는 Unity 기반의 VR 디펜스 슈팅 게임으로, 플레이어는 VR 컨트롤러를 통해 무기를 조작하며 끊임없이 몰려오는 적들을 방어합니다.
적이 본진(Core)에 도달하지 못하게 막는 것이 목표입니다.

---

## 시연 영상

[시연 영상 보기](https://youtu.be/MuP1mdIqHVw)

---

## 주요 기능

| 시스템          | 기능 설명                                      |
| ------------ | ------------------------------------------ |
| 총기 시스템       | VR에서 무기를 잡고, 발사하고, 리로드하는 전반적인 시스템          |
| 적 AI/웨이브 시스템 | 점점 증가하는 수의 적(Mob)을 스폰하고, Core를 향해 이동하게 함   |
| 피격 판정 및 이펙트  | 적이 피격되면 VFX, SFX, 진동 등의 피드백 제공             |
| UI 시스템       | 생존 시간, 적 처치 수, 탄약, 본진 체력 등 다양한 정보를 UI로 표시  |
| 시선 인터랙션 및 조준 | 레이저 시각화, 시선 기반 인터랙션, 텔레포트 커서 등 VR 인터페이스 구성 |

---

## 주요 스크립트 구성

### 무기 및 발사

| 스크립트                                             | 설명                                      |
| ------------------------------------------------ | --------------------------------------- |
| `Gun.cs`                                         | VR 컨트롤러로 무기를 잡고 놓는 이벤트 처리               |
| `Shooter.cs`                                     | 레이캐스트 방식으로 총 발사, 피격 판정, 이펙트 생성          |
| `Magazine.cs`                                    | 탄약 저장 및 리로드 처리 (`IReloadable` 인터페이스 구현) |
| `WeaponStand.cs`                                 | 무기를 스탠드에 꽂으면 자동 리로드 시작                  |
| `FlashLight`, `FlashLineRenderer`, `FlashVolume` | 총 발사 시 빛, 선, 후처리 효과 연출                  |
| `PlaySFX.cs`, `PlayHapticOnInteractable.cs`      | 발사 시 사운드와 햅틱 진동                         |

---

### 적 유닛(Mob) 시스템

| 스크립트                       | 설명                              |
| -------------------------- | ------------------------------- |
| `Mob.cs`                   | 적 유닛의 생성, 파괴, 본진 도달 시 이벤트 처리    |
| `MobManager.cs`            | 모든 적 유닛을 관리하고, 일괄 제거 기능 제공      |
| `Spawner.cs`               | 시간이 지날수록 점점 더 많은 적을 스폰 (웨이브 기반) |
| `RandomAgentSpeedRatio.cs` | 적마다 이동 속도 랜덤화                   |
| `RandomColor.cs`           | 적 이펙트/재질 색상 랜덤화                 |

---

### 본진(Core) 방어

| 스크립트                                                     | 설명                                |
| -------------------------------------------------------- | --------------------------------- |
| `Core.cs`                                                | 본진의 체력 관리, 적 도달 시 피해 처리 및 게임오버 조건 |
| `ChangeAgentDestination`, `ChangeAgentDestinationToCore` | 적의 목표 지점 설정 (예: Core)             |

---

### 인터랙션 / 피드백

| 스크립트                  | 설명                              |
| --------------------- | ------------------------------- |
| `Hittable.cs`         | 피격 가능한 오브젝트 인터페이스 (Hit 이벤트 발생)  |
| `ActivateOnLookAt.cs` | 시선이 일정 시간 머무르면 대상 활성화           |
| `EventBridge.cs`      | 유니티 이벤트를 외부에서 트리거할 수 있게 연결      |
| `ReturnToTarget.cs`   | 오브젝트가 천천히 타겟 위치로 돌아가도록 애니메이션 처리 |

---

### 조준 및 시각화

| 스크립트                       | 설명                                 |
| -------------------------- | ---------------------------------- |
| `RayVisualizer.cs`         | 레이저(LineRenderer) 및 표적(Reticle) 표시 |
| `TeleportActionHandler.cs` | 입력 액션을 통해 텔레포트 시각화 토글              |

---

### UI 시스템

| 스크립트                      | 설명                         |
| ------------------------- | -------------------------- |
| `MobCounterUI.cs`         | Kill / Alive / Spawn 정보 표시 |
| `SurvivalTimeUI.cs`       | 생존 시간 실시간 표시               |
| `Core.cs` + `OnHpChanged` | Core 체력 정보를 문자열 형태로 전달     |

---

## 의존성 및 기술 스택

* Unity 2021 이상
* XR Interaction Toolkit
* TextMeshPro
* NavMesh Agent
* UnityEvents 기반 인터랙션 구조
* VR 디바이스 (Meta Quest 등) 사용 권장

---

## 사용 방법

1. Unity 프로젝트 열기
2. `XR Rig`를 VR 설정에 맞게 구성
3. `Spawner` 오브젝트를 `Scene`에 배치하여 적 스폰 시작
4. `Gun` 오브젝트를 `WeaponStand`에 연결하거나 직접 잡아 발사 가능
5. `Core` 오브젝트를 씬에 배치하여 본진 역할 수행

---

## 시연 영상 다시 보기

[https://youtu.be/MuP1mdIqHVw](https://youtu.be/MuP1mdIqHVw)
