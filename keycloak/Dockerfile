# Étape de build
FROM maven:3.9.6-eclipse-temurin-17@sha256:29a1658b1f3078e07c2b17f7b519b45eb47f65d9628e887eac45a8c5c8f939d4 AS builder
WORKDIR /app
# Copie du fichier pom.xml
COPY kc-groupid-mapper/pom.xml .
RUN mvn -B -q -e -DskipTests dependency:go-offline
# Copie des sources
COPY kc-groupid-mapper/src ./src
RUN mvn -B -q -DskipTests package

# Importation du module dans keycloak
FROM quay.io/keycloak/keycloak:26.5.1@sha256:b80a48090594367bd8cf6fe2019466ac4ea49de4d0830fb2a43256eda37b18f5
WORKDIR /opt/keycloak
COPY --from=builder /app/target/kc-groupid-mapper-*.jar /opt/keycloak/providers/
RUN /opt/keycloak/bin/kc.sh build
