# Render 배포 가이드

## 1. Render 설정
1. render.com 회원가입
2. GitHub 저장소 연결
3. Web Service 생성

## 2. 빌드 설정
```yaml
# render.yaml
services:
  - type: web
    name: reviewpage
    env: node
    plan: free  # 또는 starter ($7/월)
    buildCommand: npm run build
    startCommand: npm start
    envVars:
      - key: NODE_ENV
        value: production
      - key: PORT
        value: 10000
      - key: DATABASE_URL
        fromDatabase:
          name: reviewpage-db
          property: connectionString
      - key: JWT_SECRET
        generateValue: true
      - key: JWT_EXPIRES_IN
        value: 7d

databases:
  - name: reviewpage-db
    plan: free  # 무료 PostgreSQL (90일 후 삭제)
```

## 3. 환경 변수
Render 대시보드에서 설정:
- `JWT_SECRET`: 자동 생성
- `FRONTEND_URL`: Render 도메인
- `DATABASE_URL`: 자동 연결

## 4. 주의사항
- 무료 플랜: 15분 비활성 시 스핀다운
- 유료 플랜($7/월): 24/7 운영

## 비용: 무료 또는 $7/월