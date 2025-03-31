![image](https://github.com/user-attachments/assets/b2056d9b-6652-41c3-9e0e-c671a2833d27)


기본 Ray Tracer를 기반으로, **Phong 조명 모델**과 **그림자(shadow)**를 적용하여  
사실적인 입체감과 광원 반응을 구현합니다.

---

 구성 요소 요약

- **광원 (Light Source)**
  - 위치: `(-4, 4, -3)`
  - 단일 흰색 포인트 라이트 (감쇠 없음)

- **재질 (Material)**
  - 각 오브젝트별로 `ka`, `kd`, `ks`, `specular power` 값이 다르게 설정됨
  - 예: Sphere S2는 `specular` 반사를 가짐 (`ks ≠ 0`, `power = 32`)

- **Phong Lighting 구성**
  - `Ambient`: 주변광 (항상 존재)
  - `Diffuse`: 입사광과 표면 노멀의 각도에 따른 확산광
  - `Specular`: 반사광 (하이라이트)

---

 조명 계산 방식

각 픽셀마다 광선(ray)을 쏴서 물체에 닿는 경우:

```cpp
color = ka + kd * max(N·L, 0) + ks * pow(max(N·H, 0), specular_power);
