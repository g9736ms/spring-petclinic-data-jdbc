# Spring PetClinic Sample Application built with Spring Data JDBC

# QuickStart
## Build 방법
```shell
./gradle build
```

### Jib 이용 방법 
gradlew jib 를 이용하여 이미지 build + push 까지 이뤄집니다.
![alt text](https://www.publickey1.jp/2018/jib02.gif)
```shell
./gradlew jib -Djib.to.image="your/repo" \
  -Djib.to.tags="latest"
  -Djib.to.auth.username="$YOUR_REPO_ID" \
  -Djib.to.auth.password="$YOUR_REPO_PW"
```

### Helm chart 적용 방법
```
helm install my-spring-petclinic helm/spring-petclinic-data-jdbc/ -f helm/spring-petclinic-data-jdbc/values-main.yaml -n namespace
```


### Github Action
시큐어 코딩을 이용하기 위해서 github 의 secrets 을 이용해야 합니다. 배포시 argocd 를 이용한다고 가정했습니다.

### 주요 동작 설명
```
[build-push]
- main 브랜치에 app/** 의 코드가 바뀌면 빌드 시작됩니다.
- Gradle wrapper 로 유효성을 검증
- ./gradlew jib 명령어로 이미지 빌드 그리고 push
- Kubernetes의 helm 매니페스트를 tags 변경

[deploy-argocd]
- 해당 APP의 Deployment 오브젝트에 대해 Sync 를 맞춰 줍니다.
```
![alt text](https://3365.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fb33c6cf3-ff8d-49a2-8cfb-219399db8f44%2F37c4847f-b618-45a2-a314-13c7eca0a7ae%2F%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2024-02-13_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.48.17.png?table=block&id=050c2d8a-a375-4860-839c-af00d700b28f&spaceId=b33c6cf3-ff8d-49a2-8cfb-219399db8f44&width=2000&userId=&cache=v2)
