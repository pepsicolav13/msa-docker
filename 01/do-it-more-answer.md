# Do it more 정답

## 01 #1

```bash
docker run -d nginx

docker exec $COND_ID apt update
docker exec $COND_ID apt install -y wget
echo hello > hello.txt
docker cp hello.txt $COND_ID:/usr/share/nginx/html/
docker exec $COND_ID wget localhost/hello.txt
docker cp $COND_ID:/hello.txt $HOME/hello.txt
cat $HOME/hello.txt
```

## 02 #1

```bash
docker run -p 8080:8080 -p 50000:50000 jenkins
```

## 02 #2

```bash
docker run centos cat /etc/os-release
docker run centos yum install -y python38
```


## 03 #1

```java
public class Hello {

    public static void main(String[] args) throws Exception {
        System.out.println("Hello");
    }
}
```

```bash
javac Hello.java
```

```bash
FROM openjdk:8-jdk-alpine
COPY Hello.class .
CMD ["java", "Hello"]
```

```bash
docker build . -t hello
docker run hello
```

## 03 #2

```bash
FROM openjdk:11.0.13-jdk

COPY Web.java .
RUN javac Web.java
CMD ["java", "Web"]
```

```bash
docker build . -t web
docker run -p 8000:8000 web
```

## 03 #3


Dockerfile 생략 (위와 거의 비슷함.)

```bash
docker build . -t read
docker run -v $PWD:/tmp read java Read /tmp/Dockerfile
```


## 04 #1

base, social Dockerfile 둘다 동일

- single-stage:

```bash
# Dockerfile
FROM openjdk:8-jdk-alpine
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
CMD ["java","-jar","/app.jar"]
```

---

- multi-stage:

```bash
# Dockerfile
FROM maven:3.6.0-jdk-8-slim AS build
COPY src /home/app/src
COPY pom.xml /home/app
RUN mvn -f /home/app/pom.xml clean package -Dmaven.test.skip

#
# Package stage
#
FROM openjdk:8-jdk-alpine
COPY --from=build /home/app/target/*.jar /app.jar
CMD ["java","-jar","/app.jar"]
```

```bash
# base directory에서 다음 명령 실행
docker build . -t base

# social directory에서 다음 명령 실행
docker build . -t social

docker run -p 8080:8080 base
docker run -p 8081:8081 social
```

## 04 #2

### base project

```bash
vim src/main/java/com/msa/repository/FollowRestRepository.java
# localhost --> social

vim src/main/java/com/msa/repository/FeedRestRepository.java
# localhost --> social
```

### social project

```bash
vim src/main/java/com/msa/repository/AuthTokenRestRepository.java
# localhost --> base
```

```bash
# $(hostname -i) 대신에 실제 서버 IP를 넣어도 됨.

docker run --add-host="social:$(hostname -i)" -p 8080:8080 base

docker run --add-host="base:$(hostname -i)" -p 8081:8081 social
```
