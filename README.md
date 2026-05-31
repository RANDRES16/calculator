# calculator
Test book Continuous Delivery with Docker and Jenkins

# Práctica Capítulo 4 – Jenkins CI/CD con Java Spring Boot

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Coverage](https://img.shields.io/badge/coverage-100%25-brightgreen)
![Java](https://img.shields.io/badge/java-17-blue)
![Maven](https://img.shields.io/badge/maven-3.9.0-blue)

**Estudiante:** Rene Palta  
**Fecha:** 30 de mayo de 2026  
**Libro:** Continuous Delivery with Docker and Jenkins, 3rd Edition  

---

## 📋 Descripción

Esta práctica implementa un **Pipeline de Integración Continua** para una aplicación Java Spring Boot simple: una calculadora que suma dos números.  

Se automatizaron:

- Compilación
- Pruebas unitarias
- Cobertura de código (JaCoCo)
- Análisis estático de código (Checkstyle)
- Análisis de calidad (SonarQube)
- Notificaciones por correo electrónico
- Ejecución automática mediante GitHub Webhook

---

## 🚀 Tecnologías utilizadas

| Tecnología | Versión/Detalle |
|------------|----------------|
| Jenkins | Docker Container |
| Java | 17 |
| Maven | 3.x |
| JaCoCo | Maven plugin |
| Checkstyle | Maven plugin |
| SonarQube | Local / Docker |
| GitHub | SCM & Webhooks |

---

## 📂 Estructura del proyecto
calculator/
├── src/
│ ├── main/java/com/oreilly/calculator/...
│ └── test/java/com/oreilly/calculator/...
├── pom.xml
├── Jenkinsfile
├── README.md
└── RESPUESTAS_CAPITULO_4.md


---

## 🏗 Pipeline de Jenkins

### Etapas principales

1. **Compile**
    ```bash
    ./mvnw compile
    ```
2. **Unit Test**
    ```bash
    ./mvnw test
    ```
3. **Code Coverage**
    ```bash
    ./mvnw verify
    ```
    - Genera reportes en `target/site/jacoco/`.
    - Jenkins publica el HTML usando **HTML Publisher Plugin**.
4. **Static Analysis**
    ```bash
    ./mvnw checkstyle:checkstyle
    ```
    - Detecta errores de estilo según `checkstyle.xml`.
5. **SonarQube Analysis**
    ```bash
    ./mvnw sonar:sonar
    ```
    - Envía métricas de cobertura y calidad a SonarQube.

---

### 🔔 Post Actions / Notificaciones

```groovy
post {
    always {
        mail(
            to: 'team@company.com',
            subject: "Pipeline completado: ${currentBuild.fullDisplayName}",
            body: "Revisar resultados: ${env.BUILD_URL}"
        )
    }
}
