---
layout: post
title:  "[React] 개발 환경 설정"
date:   2019-05-18 00:53:07
categories: react
tags: react
image: 
---

# React

## Global Dependncy 설치
`$sudo npm install -g webpack webpack-dev-serer`
- webpack : 브라우저 위에서 import(require)를 할 수 있게 해주고 자바스킙트 파일들을 하나로 합쳐준다.
- webpack-dev-server : 별도의 서버를 구축하지 않고도 static 파일을 다루는 웹서버를 열 수 있으며 hot-loader를 통하여 코드가 수정 될 때마다 자동으로 리로드 되게 할 수 있습니다.


## 프로젝트 생성
> $mkdir react-fundamentals  
> $cd react-fundamentals  
> $npm init


## Dependency 및 Plugin 설치
React 설치
- npm install --save react react-dom  

개발 의존 모듈 설치
- npm install --save-dev babel-core babel-loader babel-preset-es2015 babel-preset-react
- npm install --save-dev react-hot-loader webpack webpack-dev-server 

## Webpack 설치
- webpack.config.js 파일 만들기