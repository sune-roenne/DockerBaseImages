FROM eclipse-temurin:22-jammy as app
COPY --chown=1 proxy-root.crt /usr/local/share/ca-certificates/proxy-root.pem
COPY --chown=1 forti-proxy.crt /usr/local/share/ca-certificates/forti-proxy.pem
RUN apt update
RUN apt-get install -y ca-certificates
RUN update-ca-certificates
RUN keytool -import -trustcacerts -keystore /opt/java/openjdk/lib/security/cacerts -storepass changeit -noprompt -alias proxyroot -file /usr/local/share/ca-certificates/proxy-root.pem
RUN keytool -import -trustcacerts -keystore /opt/java/openjdk/lib/security/cacerts -storepass changeit -noprompt -alias fortiproxy -file /usr/local/share/ca-certificates/forti-proxy.pem
ENTRYPOINT ["tail", "-f", "/dev/null"]

