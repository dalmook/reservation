# 점핑배틀 NAS + GitHub Pages 운영센터

구글시트 없이 Synology NAS와 GitHub Pages로 운영하는 버전입니다.

## 포함 기능
- 관리자 PIN 로그인
- 실시간 방/시간대 예약 현황
- 현재 시간 기준 다음 20분 슬롯 파란색 하이라이트
- 예약 추가/수정/취소
- 결제 추가
- 슬러쉬/음료/양말 상품 추가
- 슬롯 추가/삭제/막기/열기
- 방 추가/수정
- 운영시간 시작/종료/간격 변경
- 일자 초기화와 백업
- 매출/팀수/인원/객단가/점유율 분석
- 시간대별/방별/난이도별/결제수단 차트
- CSV 내보내기

## NAS 배포
```bash
cd /volume1/docker
unzip jumpingbattle_nas_web_pro.zip
cd jumpingbattle_nas_web_pro

cat > .env <<'EOF'
JWT_SECRET=change-this-long-random-secret
ADMIN_PIN=1234
CORS_ORIGIN=*
SHOP_NAME=점핑배틀
EOF

docker compose up -d --build
```

확인:
```bash
curl http://jump.dalbong2.synology.me:18090/health
```

## GitHub Pages 배포
`frontend` 폴더 안의 파일을 GitHub Pages 저장소 루트에 올립니다.

`frontend/config/default.json` 수정:
```json
{
  "apiBase": "http://jump.dalbong2.synology.me:18090",
  "shopName": "점핑배틀"
}
```

외부 접속까지 하려면 NAS Reverse Proxy/HTTPS/방화벽/포트포워딩 설정이 필요합니다.

## 시판 품질 고도화 체크리스트
- HTTPS reverse proxy
- 직원/관리자 권한 분리
- 감사 로그 화면
- 백업 파일 다운로드/복원
- 네이버 예약 수집 API 연결
- 키오스크 고객용 화면 분리
- 영수증/POS 출력
- 알림톡/문자 발송
- PostgreSQL 옵션
- 멀티 지점
Code → README.md → 연필 아이콘 → 맨 아래 빈 줄 하나 추가 → Commit changes
