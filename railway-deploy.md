# Railway 배포 가이드

## 1. Railway 프로젝트 생성
```bash
# Railway CLI 설치
npm install -g @railway/cli

# 로그인
railway login

# 프로젝트 생성
railway new
```

## 2. 환경 변수 설정
Railway 대시보드에서 설정:
```env
NODE_ENV=production
PORT=3001
DATABASE_URL=(Railway PostgreSQL 자동 생성)
JWT_SECRET=your-production-jwt-secret-key
JWT_EXPIRES_IN=7d
FRONTEND_URL=https://your-app-name.up.railway.app
```

## 3. railway.toml 생성
```toml
[build]
builder = "NIXPACKS"

[deploy]
restartPolicyType = "ON_FAILURE"
restartPolicyMaxRetries = 10

[[services]]
name = "web"
source = "."

[services.web]
buildCommand = "npm run build"
startCommand = "npm start"
```

## 4. 배포 실행
```bash
# 첫 배포
railway up

# 이후 Git push로 자동 배포
git push origin main
```

## 비용: $5/월 (PostgreSQL 포함)