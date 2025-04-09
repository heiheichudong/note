FROM openjdk:11

# 设置工作目录
WORKDIR /code

COPY ./edu-gateway-0.0.1-SNAPSHOT.jar /code/edu-gateway-0.0.1-SNAPSHOT.jar
COPY ./edu-oauth-0.0.1-SNAPSHOT.jar /code/edu-oauth-0.0.1-SNAPSHOT.jar
COPY ./edu-server-resource-0.0.1-SNAPSHOT.jar /code/edu-server-resource-0.0.1-SNAPSHOT.jar
COPY ./edu-server-system-0.0.1-SNAPSHOT.jar /code/edu-server-system-0.0.1-SNAPSHOT.jar
COPY ./edu-server-teacher-0.0.1-SNAPSHOT.jar /code/edu-server-teacher-0.0.1-SNAPSHOT.jar
COPY ./start.sh /code/start.sh

# 给予启动脚本执行权限
RUN chmod +x /start.sh

# 暴露端口
EXPOSE 8001 8101 8203 8201 8204
#EXPOSE 8101
#EXPOSE 8203
#EXPOSE 8201
#EXPOSE 8204

# 使用启动脚本启动多个服务
CMD ["/start-services.sh"]