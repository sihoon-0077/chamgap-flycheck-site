# chamgap-flycheck-site

참값 × FlyCheck 정적 문서 사이트입니다(설계서 41장). Vercel이 이 저장소의 `main` 브랜치를 배포합니다.

| 경로 | 내용 |
|---|---|
| `/` | 안내 페이지 |
| `/results` | 결과 대시보드. HTML은 고정이고 `results/data/`의 파일만 교체합니다 |
| `/parts` | 부품 목록, 역할, 배선·물길 연결도. `parts/data/parts.json`만 교체합니다. 연결도는 검토용 제안(실물 검수 전)입니다 |

부품 데이터는 `chamgap_v4/`에서 `python -m experiments.export_site_parts --out <이 저장소>/parts/data`로 만듭니다. 수량·가격·링크는 구매 CSV에서 그대로 가져오고, 합계를 설계서 소계와 대조합니다.

## 데이터 갱신

`chamgap_v4/`에서 실행합니다.

```bash
python -m experiments.export_site_data --out <이 저장소>/results/data --master "<설계서 .md 경로>"
```

그다음 `results/data/results.json`과 `results/data/learning_curve.csv`를 커밋하고 푸시하면 Vercel이 자동으로 다시 배포합니다. 두 파일에는 생성 일시, `code_sha256`, `domain`이 들어 있습니다.

## 읽을 때 주의

- `domain=SIM_ONLY_UNCALIBRATED…`는 보정되지 않은 가상 시뮬레이터 결과입니다. 현장 성능이 아닙니다.
- `connectome=DEMO_RANDOM_NOT_BIOLOGICAL`은 난수 연결입니다. 실제 초파리 연결이 아닙니다.

## 로컬 확인

```bash
python -m http.server 8765
# http://localhost:8765/results/
```

파일을 직접 열면(`file://`) 브라우저가 데이터 파일을 읽지 못합니다.
