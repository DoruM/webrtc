FROM kaazing/development-enterprise-gateway:develop-SNAPSHOT

# Generate Keystore entry for kaazing.example.com

RUN keytool -genkeypair -keystore conf/keystore.db -storetype JCEKS -keypass ab987c -storepass ab987c -alias kaazing.example.com -keyalg RSA -dname "CN=kaazing.example.com, OU=Example, O=Example, L=Mountain View, ST=California, C=US"

RUN keytool -exportcert -alias kaazing.example.com -keystore conf/keystore.db -storetype JCEKS -file conf/hostname.cer -storepass ab987c
RUN keytool -importcert -keystore conf/truststore.db -storepass changeit -storetype JCEKS -alias kaazing.example.com -file conf/hostname.cer -noprompt

RUN apt-get update
RUN apt-get install -y netcat
RUN apt-get install -y dnsutils

# Add jms client libraries
ADD http://central.maven.org/maven2/org/apache/activemq/activemq-client/5.10.0/activemq-client-5.10.0.jar lib/ext/
ADD http://central.maven.org/maven2/org/apache/geronimo/specs/geronimo-jms_1.1_spec/1.1/geronimo-jms_1.1_spec-1.1.jar lib/ext/
ADD http://central.maven.org/maven2/org/apache/geronimo/specs/geronimo-j2ee-management_1.1_spec/1.0.1/geronimo-j2ee-management_1.1_spec-1.0.1.jar lib/ext/
ADD http://central.maven.org/maven2/org/fusesource/hawtbuf/hawtbuf/1.11/hawtbuf-1.11.jar lib/ext/

# Add gateway config
COPY gateway-config.xml conf/gateway-config.xml
COPY log4j-config.xml conf/log4j-config.xml
COPY web/webrtc web/webrtc

