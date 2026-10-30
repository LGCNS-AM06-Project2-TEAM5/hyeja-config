# hyeja-config

혜자 MSA(5조)의 Spring Cloud Config Server가 읽는 설정 저장소입니다. (공통 요구사항 4번)

- 서버: [hyeja-msa/infra/config-service](https://github.com/__ORG__/hyeja-msa/tree/develop/infra/config-service)
- 조회 예: `GET http://localhost:8888/member-service/dev`

## 파일 규칙

| 파일 | 적용 대상 |
|---|---|
| `application.yml` | 모든 서비스 공통 |
| `application-{profile}.yml` | 모든 서비스의 해당 프로필 (`local`, `dev`, `prod`) |
| `{서비스이름}.yml` | 해당 서비스 공통 |
| `{서비스이름}-{profile}.yml` | 해당 서비스의 해당 프로필 |

서비스 이름은 각 서비스의 `spring.application.name`과 같아야 합니다.

## 비밀값

- 이 저장소에 비밀값을 평문으로 넣지 않습니다.
- DB 비밀번호, API 키 등은 Config Server의 `/encrypt`로 암호화한 뒤 `'{cipher}암호문'` 형식으로 넣습니다. (선택 요구사항 2번)
- 설정을 바꾼 뒤 `POST /actuator/busrefresh`로 연결된 서비스에 한 번에 반영합니다. (선택 요구사항 1번)
