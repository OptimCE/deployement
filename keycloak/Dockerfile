# Étape de build
FROM maven:3.9.12-eclipse-temurin-17@sha256:a0603aab698040d9c94259f379ec0487da1678560748d6c7508483034033c53d AS builder
WORKDIR /app
# Copie du fichier pom.xml
COPY kc-groupid-mapper/pom.xml .
RUN mvn -B -q -e -DskipTests dependency:go-offline
# Copie des sources
COPY kc-groupid-mapper/src ./src
RUN mvn -B -q -DskipTests package

# Importation du module dans keycloak
FROM quay.io/keycloak/keycloak:26.5.5@sha256:a7b0cb7a43a1235a61872883414d3f1d9a3ceac9df6e5907bd12202778a6265c
WORKDIR /opt/keycloak
COPY --from=builder /app/target/kc-groupid-mapper-*.jar /opt/keycloak/providers/
RUN /opt/keycloak/bin/kc.sh build
