# Build from ./..
FROM sbtscala/scala-sbt:eclipse-temurin-jammy-22_36_1.10.3_3.5.2 as build
WORKDIR /appres
COPY proxy-root.crt /usr/local/share/ca-certificates/proxy-root.pem
COPY forti-proxy.crt /usr/local/share/ca-certificates/forti-proxy.pem
RUN apt-get install ca-certificates
RUN update-ca-certificates
RUN keytool -import -trustcacerts -keystore /opt/java/openjdk/lib/security/cacerts -storepass changeit -noprompt -alias proxyroot -file /usr/local/share/ca-certificates/proxy-root.pem
RUN keytool -import -trustcacerts -keystore /opt/java/openjdk/lib/security/cacerts -storepass changeit -noprompt -alias fortiproxy -file /usr/local/share/ca-certificates/forti-proxy.pem
COPY ScalaPekko/build.sbt build.sbt
COPY ScalaPekko/project/plugins.sbt project/plugins.sbt
COPY ScalaPekko/.sbtopts .sbtopts
ENV http_proxy http://webproxy.nykreditnet.net:8080/
ENV https_proxy http://webproxy.nykreditnet.net:8080/
RUN sbt update
ENTRYPOINT ["tail", "-f", "/dev/null"]
