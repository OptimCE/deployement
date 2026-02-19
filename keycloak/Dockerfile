# Étape de build
FROM maven:3.9.6-eclipse-temurin-17 AS builder
WORKDIR /app
# Copie du fichier pom.xml
COPY kc-groupid-mapper/pom.xml .
RUN mvn -B -q -e -DskipTests dependency:go-offline
# Copie des sources
COPY kc-groupid-mapper/src ./src
RUN mvn -B -q -DskipTests package

# Importation du module dans keycloak
FROM quay.io/keycloak/keycloak:26.5.1
WORKDIR /opt/keycloak
COPY --from=builder /app/target/kc-groupid-mapper-*.jar /opt/keycloak/providers/
RUN /opt/keycloak/bin/kc.sh build
