# spring boot 程序部署到docker
## 1. 编写docker 文件
```
FROM openjdk:8-jre-slim
MAINTAINER weiyixiao

ENV PARAMS=""

ENV TZ=PRC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ADD target/gaia-wei-common.jar /app.jar

EXPOSE 8980

ENTRYPOINT ["sh","-c","java -jar $JAVA_OPTS /app.jar $PARAMS"]
```
> 其中 FROM 配置基础镜像
> MAINTAINER 表示创建者名称

对应的目录结构：
```
├── Dockerfile
├── pom.xml
├── src
    ├── main
    │   ├── java
    │   └── resources
    │       ├── application.yml
    │       └── logback-spring.xml
    └── test
        └── java
```

## 2.在项目的根据路径（也就是Dockerfile）执行docker部署命令
```
docker build -t wei-common/gaia-wei-common:1.0.1 -f Dockerfile .
```
> -t 指定包的tag 标签，可以通过标签来获取指定版本。
> -f Dockerfile 指定的是我们刚才编辑的docker 文件
> . 表示当前目录
## 未完成