# Práctica Capítulo 4

## Continuous Delivery with Docker and Jenkins, 3rd Edition

**Estudiante:** Rene Palta
**Fecha:** 30 de mayo de 2026
**Capítulo:** 4
**Tema:** Jenkins Pipeline, Cobertura de Código, Análisis Estático y Automatización

---

# Respuestas – Jenkins Pipeline y DevOps

## 1. ¿Qué es un Pipeline?

Un Pipeline es un flujo de trabajo automatizado que define las etapas y tareas necesarias para construir, probar, analizar y desplegar una aplicación. En Jenkins, un Pipeline permite implementar prácticas de Integración Continua (CI) y Entrega Continua (CD), automatizando actividades que normalmente se realizarían de forma manual.

Ejemplo de flujo:

```text
Git Push
   ↓
Compilación
   ↓
Pruebas Unitarias
   ↓
Cobertura de Código
   ↓
Análisis Estático
   ↓
Despliegue
```

---

## 2. ¿Cuál es la diferencia entre una Stage y un Step en un Pipeline?

### Stage (Etapa)

Una Stage representa una fase importante dentro del Pipeline. Sirve para organizar el proceso en bloques lógicos.

Ejemplos:

* Compile
* Unit Test
* Code Coverage
* Static Analysis

### Step (Paso)

Un Step es una acción específica que se ejecuta dentro de una Stage.

Ejemplo:

```groovy
stage('Unit Test') {
    steps {
        sh './mvnw test'
    }
}
```

En este caso:

* `Unit Test` es la Stage.
* `sh './mvnw test'` es el Step.

---

## 3. ¿Qué es la sección Post en un Jenkins Pipeline?

La sección `post` permite ejecutar acciones una vez que el Pipeline o una Stage han finalizado.

Se utiliza comúnmente para:

* Enviar notificaciones por correo.
* Publicar reportes.
* Limpiar archivos temporales.
* Ejecutar tareas posteriores al build.

Ejemplo:

```groovy
post {
    failure {
        mail(
            to: 'equipo@empresa.com',
            subject: 'Build fallido',
            body: 'Revisar Jenkins'
        )
    }
}
```

---

## 4. ¿Cuáles son las tres etapas más fundamentales del Commit Pipeline?

Las tres etapas fundamentales son:

### 1. Compilación (Compile)

Verifica que el código fuente pueda construirse correctamente.

### 2. Pruebas Unitarias (Unit Test)

Ejecuta pruebas automáticas para validar el comportamiento del código.

### 3. Análisis Estático de Código (Static Code Analysis)

Evalúa la calidad del código mediante herramientas como Checkstyle, identificando errores y malas prácticas.

---

## 5. ¿Qué es un Jenkinsfile?

Un Jenkinsfile es un archivo de texto que contiene la definición completa del Pipeline utilizando código.

Este archivo se almacena dentro del repositorio Git, permitiendo:

* Versionar el Pipeline.
* Compartirlo con el equipo.
* Mantener la infraestructura como código.

Ejemplo:

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './mvnw compile'
            }
        }
    }
}
```

---

## 6. ¿Cuál es el propósito de la etapa de Cobertura de Código?

La etapa de Cobertura de Código permite medir qué porcentaje del código de la aplicación es ejecutado por las pruebas automatizadas.

Sus objetivos principales son:

* Detectar código sin pruebas.
* Mejorar la calidad del software.
* Reducir errores en producción.
* Garantizar un nivel mínimo de cobertura.

En esta práctica se utilizó la herramienta JaCoCo para generar los reportes de cobertura.

---

## 7. ¿Cuál es la diferencia entre los triggers External y Polling SCM en Jenkins?

### External Trigger

El Pipeline es ejecutado por un evento externo.

Ejemplos:

* GitHub Webhook.
* API REST.
* Scripts externos.

Flujo:

```text
Git Push
   ↓
GitHub Webhook
   ↓
Jenkins
```

### Polling SCM

Jenkins consulta periódicamente el repositorio para verificar si existen cambios.

Ejemplo:

```text
Cada 5 minutos:
    Revisar repositorio Git
```

Si detecta cambios, ejecuta el Pipeline.

### Diferencias

| External Trigger    | Polling SCM           |
| ------------------- | --------------------- |
| Basado en eventos   | Basado en tiempo      |
| Respuesta inmediata | Puede existir retraso |
| Más eficiente       | Consume más recursos  |

---

## 8. ¿Cuáles son los métodos de notificación más comunes en Jenkins? Mencione al menos tres.

Los métodos de notificación más utilizados son:

1. Correo electrónico (SMTP).
2. Slack.
3. Microsoft Teams.

Otros métodos comunes incluyen:

* Discord.
* Telegram.
* Webhooks.
* Sistemas de monitoreo.

---

## 9. ¿Cuáles son los tres flujos de trabajo de desarrollo más comunes?

### 1. Feature Branch Workflow

Cada nueva funcionalidad se desarrolla en una rama independiente.

Ejemplo:

```text
main
 ├── feature-login
 ├── feature-payment
 └── feature-search
```

### 2. Gitflow Workflow

Utiliza varias ramas con propósitos específicos:

```text
main
develop
feature/*
release/*
hotfix/*
```

Es ampliamente utilizado en proyectos empresariales.

### 3. Trunk-Based Development

Los desarrolladores integran frecuentemente sus cambios en una única rama principal.

```text
main
```

Es un enfoque muy popular en entornos DevOps modernos.

---

## 10. ¿Qué es un Feature Toggle?

Un Feature Toggle (o Feature Flag) es una técnica que permite habilitar o deshabilitar funcionalidades sin necesidad de realizar un nuevo despliegue de la aplicación.

Ejemplo:

```java
if (featureEnabled) {
    mostrarNuevaInterfaz();
} else {
    mostrarInterfazAnterior();
}
```

### Beneficios

* Despliegues más seguros.
* Activación gradual de funcionalidades.
* Pruebas A/B.
* Desactivación rápida de características problemáticas.

Flujo típico:

```text
Funcionalidad desplegada
        ↓
Funcionalidad desactivada
        ↓
Activación para un porcentaje de usuarios
        ↓
Activación para todos los usuarios
```

Esta técnica es ampliamente utilizada en prácticas modernas de Entrega Continua (Continuous Delivery).

---

## Conclusión

Durante esta práctica se implementó un Pipeline de Integración Continua utilizando Jenkins y Maven para una aplicación Java Spring Boot. Se configuraron etapas de compilación, pruebas unitarias, cobertura de código mediante JaCoCo, análisis estático con Checkstyle y ejecución automática mediante Webhooks de GitHub. Estas prácticas permiten mejorar la calidad del software, automatizar procesos y aplicar principios fundamentales de DevOps y Continuous Delivery.

