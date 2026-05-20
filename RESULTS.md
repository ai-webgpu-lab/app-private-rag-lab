# Results

## 1. 실험 요약
- 저장소: app-private-rag-lab
- 커밋 해시: 31f1eea
- 실험 일시: 2026-05-20T15:34:29.608Z -> 2026-05-20T15:34:32.823Z
- 담당자: ai-webgpu-lab
- 실험 유형: `integration`
- 상태: `success`

## 2. 질문
- 내부 데모 surface에서 private-note ingest, retrieve, answer 흐름을 한 번에 검증할 수 있는가
- local-only 상태와 citation hit-rate가 앱 결과 문서에 함께 남는가
- 실제 embedder/generator/provider 연결 전 private RAG app protocol을 고정할 수 있는가

## 3. 실행 환경
### 브라우저
- 이름: Chrome
- 버전: 147.0.7727.15

### 운영체제
- OS: Linux
- 버전: unknown

### 디바이스
- 장치명: Linux x86_64
- device class: `desktop-high`
- CPU: 16 threads
- 메모리: 32 GB
- 전원 상태: `unknown`

### GPU / 실행 모드
- adapter: not-applicable
- backend: `browser-fixture`
- fallback triggered: `false`
- worker mode: `main`
- cache state: `warm`
- required features: []
- limits snapshot: {}

## 4. 워크로드 정의
- 시나리오 이름: Private RAG Lab
- 입력 프로필: 4-private-notes-4-questions
- 데이터 크기: private fixture; docs=4; chunks=9; questions=4; local_only=true; automation=playwright-chromium, private fixture; docs=4; chunks=9; questions=4; local_only=true; realAdapter=fallback(manifest fetch failed for https://ai-webgpu-lab.github.io/app-private-rag-lab/manifests/corpus-v1.json); automation=playwright-chromium
- dataset: private-notes-fixture-v1
- model_id 또는 renderer: private-notes-fixture-v1
- 양자화/정밀도: -
- resolution: -
- context_tokens: -
- output_tokens: -

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 257.9 ~ 356.2 ms
- init_ms: 9.3 ~ 12.9 ms
- success_rate: 1
- peak_memory_note: 32 GB reported by browser
- error_type: -

### RAG
- ingest_ms_per_page: 0 ~ 0.02 ms
- chunk_count: 9
- embed_total_ms: 9.3 ~ 12.9 ms
- retrieve_ms: 0.1 ~ 0.25 ms
- rerank_ms: 0.02 ~ 0.37 ms
- answer_total_ms: 29.6 ms
- citation_hit_rate: 1

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | Private RAG Lab | browser-fixture | warm | 29.6 | 17.3 | retrieve=0.25 ms, citation_hit_rate=1 |
| 2 | Private RAG Lab | browser-fixture | warm | 29.6 | 17.05 | retrieve=0.1 ms, citation_hit_rate=1 |

## 7. 관찰
- private RAG lab demo는 answer_total_ms=29.6 ms, citation_hit_rate=1로 기록됐다.
- local-only app surface가 ingest, retrieve, rerank, answer 지표를 같은 결과 문서에 남긴다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. Real Adapter vs Deterministic
- adapter: real=not-connected (no real adapter registered — falling back to deterministic), deterministic=deterministic-observatory
- citation_hit_rate: real=1, deterministic=1, delta=0
- answer_total_ms: real=29.6 ms, deterministic=29.6 ms, delta=0 ms

## 9. 결론
- private RAG lab demo가 generic probe를 벗어나 local-only RAG app surface와 첫 raw result를 갖게 됐다.
- 다음 단계는 deterministic private-note fixture를 실제 browser embedder, reranker, local generator로 교체하는 것이다.
- 내부 데모 승격을 위해 문서 추가/삭제, 캐시 재방문, citation UX 메모를 더 기록해야 한다.

## 10. 첨부
- 스크린샷: ./reports/screenshots/01-private-rag-lab.png, ./reports/screenshots/02-private-rag-lab-real-private-rag.png
- 로그 파일: ./reports/logs/01-private-rag-lab.log, ./reports/logs/02-private-rag-lab-real-private-rag.log
- raw json: ./reports/raw/01-private-rag-lab.json, ./reports/raw/02-private-rag-lab-real-private-rag.json
- 배포 URL: https://ai-webgpu-lab.github.io/app-private-rag-lab/
- 관련 이슈/PR: -
