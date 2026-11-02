# skunk

미국 로보틱스 / 항공(aircraft) 업계의 Functional Safety / Systems Safety Engineer 채용 동향을 추적하는 저장소입니다.
매주 월요일 오전 8시(KST)에 클라우드 에이전트(Claude Code Scheduled Routine)가 자동으로 실행되어:

1. 최근 1주일간의 로보틱스/항공 업계 테크 뉴스 및 AI 기반 기능안전(functional safety) 관련 동향을 수집
2. `data/companies.json`의 회사 DB를 최신 뉴스, 인원 규모, 펀딩 단계, 비자/영주권 스폰서십 정보로 업데이트
3. 신규 Safety Engineer 공고를 수집하고 스폰서십 여부를 기록
4. 위 내용을 하나의 HTML 리포트로 생성하여 `reports/YYYY-MM-DD.html`에 저장
5. 이메일(또는 GitHub Issue 알림)로 리포트 발송

## 구조

- `data/companies.json` — 회사 DB (아래 스키마 참고). 매주 누적/갱신됩니다.
- `reports/` — 주차별 HTML 리포트 아카이브.

## `data/companies.json` 스키마

```jsonc
[
  {
    "name": "Company Name",
    "location": "City, State",
    "region_priority": "west_coast" | "other",
    "industry": "robotics" | "aerospace" | "aircraft" | "other",
    "headcount_estimate": "approx. N (as of YYYY-MM-DD)",
    "funding_stage": "e.g. Series B / Public / ...",
    "recent_news": [
      { "date": "YYYY-MM-DD", "summary": "...", "source_url": "https://..." }
      // 최신 10개까지만 유지
    ],
    "visa_sponsorship": {
      "known": true,
      "evidence": "짧은 근거 설명",
      "source_url": "https://...",
      "last_checked": "YYYY-MM-DD"
    },
    "job_postings": [
      {
        "title": "Functional Safety Engineer",
        "date_found": "YYYY-MM-DD",
        "url": "https://...",
        "sponsorship_mentioned": true,
        "notes": "..."
      }
      // 최신 15개까지만 유지, 90일 지난 마감 공고는 정리
    ],
    "last_updated": "YYYY-MM-DD"
  }
]
```

이 저장소는 사람이 직접 수정하기보다, 스케줄된 Claude Code 루틴이 매주 커밋을 통해 갱신합니다.
