# cmd 상에서 Ice-core 실행 

: cmd 실행 위치는 Ice-core 프로젝트 root

## 1. 그레들 빌드
```
gradlew clean build -x test --refresh-dependencies
```

## 2. 스프링 부트 실행
```
java -jar -Dspring.profiles.active=cj-local-win codedeploy/ice2-core-0.0.1-SNAPSHOT.war
```


