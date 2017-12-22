# NPM

## npm 버전을 최신 버전으로 업데이트
```
	npm install -g npm 
```

	npm 2.15.9 -> 3.10.6 을 사용하면 모듈 설치가 훨씬 빨라짐
	
	기존 버전 5.5.1
	현재 최신 버전 5.6.0
	
	npm 설치되어 있는
	

## /package.json 에 프로젝트 정보를 담고 있음

### script 

	* 예약된 명령어 : start
	
		prestart , start , poststart 순으로 실행
	
	* 예약된 명령어 : test
		
		pretest, test , posttest 순으로 실행 
	
### config

	: config 필드의 값을 환경변수처럼 접근 가능
	
```
	{ "config" :  { "port" : "8080" } } 로 셋팅시
	
	
	process.env.npm_package_config_port 로 접근가능
	
```

### devDependencies
	: 개발 때에만 필요한 모듈을 여기에 명시

	: config의 production(기본값=false)이 true인 경우에는 설치하지 않음
	
* config 값 확인

	```
	npm config list -l
	```
	
* config 값 변경

	```
	npm config set production true
	```


## 확장 모듈은 글로벌(사용자 폴더),로컬(프로젝트 폴더)에 나누어 설치됨

	폴더명 : node_modules

	/usr/local/lib 하위
	사용자 폴더 \AppData\Roaming 하위
	
	npm install시 -g 옵션을 붙이면 글로벌로 설치됨
	
	
## npm 설치되어 있는 모듈 확인 방법

	* 글로벌
		npm list -g

	* 로컬
		npm list 
	
		
## nodemon -> 소스 변경시 node.js 재시작 ( 핫 디플로이는 아님 )

