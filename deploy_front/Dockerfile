# Nginx를 사용하지 않고, 로컬에서 실행시켰던 방식으로 npm run dev를 사용하는 방법
# node 버전에 맞게
# FROM node:22-alpine

# WORKDIR /app

# # package.json 를 복사해서 실행 => node_modules가 만들어짐
# COPY . .
# RUN npm install

# EXPOSE 5173

# # 접근허용
# CMD [ "npm", "run", "dev", "--", "--host" ]

# 1단계 : 빌드
# FROM node:22-alpine AS build
# WORKDIR /app

# # package.json을 통해서 의존성(패키지) 설치
# COPY package.json ./
# RUN npm install

# # 소스 코드 복사
# COPY . .

# # React 빌드 수행 (dist 폴더 생성)
# RUN npm run build

# 2단계 : 실행 환경(Nginx 환경 연결)
FROM nginx:stable-alpine

# React에 빌드 결과물은 Nginx 정적 폴더로 복사
# react의 build 도구 현재 Vite를 사용 중(dist)
# Create React App 사용한다면 build 폴더
# COPY --from=build /app/dist /usr/share/nginx/html
COPY dist /usr/share/nginx/html

# Nginx기본 설정 대신에 사용할 설정파일이 있다면 추가 COPY해주면 된다
# COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
# nginx를 실행하면 백그라운드 실행 , nginx를 컨테이너가 종료되도 실행 될 수 있도록
# 컨테이너가 시작될 때 nginx가 종료되지 않게 설정
CMD ["nginx","-g","daemon off;"]