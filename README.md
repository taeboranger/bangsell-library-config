# Bangsell Library GitOps

대상 저장소: https://github.com/taeboranger/bangsell-library-config.git

- 도메인: `bangsell.cagea1.com`
- 네임스페이스: `bangsell-library-prod`
- 이미지: `lightstone1/bangsell-library-prod`
- Vault KV v2: `kv/data/bangsell-library-secret`
- SOOP 키: `soop-username`, `soop-password` → `SOOP_LOGIN_ID`, `SOOP_LOGIN_PW`
- 추가 Vault 키: `db-host`, `db-port`, `db-name`, `db-username`, `db-password`,
  `admin-username`, `admin-password`, `worker-api-token`
- VSO 역할: `bangsell-library-vso`
- 웹/크롤러만 배포합니다. Ollama/GPU 워커는 PC에서 별도로 실행합니다.
- DB는 별도 준비하고 복원합니다. 이 config는 DB 인스턴스를 생성하거나 기존 DB를 변경하지 않습니다.

```bash
kubectl kustomize overlays/prod
# Vault/DB/이미지/DNS 준비 후 수동 적용 또는 ArgoCD 연결
kubectl apply -k overlays/prod
```

Vault 정책은 `kv/data/bangsell-library-secret` 읽기 권한과
`bangsell-library-prod/bangsell-library-vault-auth` ServiceAccount 바인딩이 필요합니다.
운영 준비·DB 이전·PC 실행에 대한 전체 절차는 프로젝트 저장소의 `docs/MIGRATION.md`를 참고하세요.
