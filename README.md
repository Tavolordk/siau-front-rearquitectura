# SIAU Frontend Re-Arquitectura

## Descripción General

Este repositorio contiene la **rearquitrectura del frontend del sistema SIAU (Sistema Integral de Administración de Usuarios)**.

El objetivo de este proyecto es reconstruir el frontend existente de SIAU utilizando una **arquitectura limpia, escalable y mantenible**, basada en buenas prácticas modernas de Angular y principios de **Domain-Driven Design (DDD)**.

En lugar de modificar progresivamente el sistema legado, este repositorio establece una **nueva base arquitectónica**, donde las funcionalidades se implementarán gradualmente respetando límites claros entre capas.

### Objetivos principales

- Mantenibilidad a largo plazo
- Separación clara de responsabilidades
- Modularidad orientada a dominios
- Estándares de desarrollo consistentes
- Escalabilidad para futuras funcionalidades

---

# Tecnologías Utilizadas

- Angular (última versión estable)
- TypeScript
- SCSS
- Angular Router
- Node.js / NPM

La aplicación utiliza **arquitectura basada en standalone components** y herramientas modernas del ecosistema Angular.

---

# Principios de Arquitectura

El sistema sigue los principios de **Clean Architecture** y **Domain-Driven Design (DDD)**.

## Reglas fundamentales

- Separación por **dominios**, no por tipo técnico.
- La capa de **presentación** no debe acceder directamente a **infraestructura**.
- La **lógica de negocio** no debe existir dentro de los componentes.
- La capa de **dominio debe ser independiente del framework**.
- El código **shared** no debe contener reglas de negocio.
- Cada dominio debe ser **autocontenible**.

Esta estructura permite que cada dominio evolucione de forma independiente sin generar acoplamiento innecesario entre módulos.

---

# Estructura del Proyecto

El código principal de la aplicación se encuentra en:
src/app

Estructura general:
app
├ core
├ shared
├ shell
├ domains
├ app.config.ts
└ app.routes.ts

---

# Capa Core

core/

Contiene funcionalidades **transversales** utilizadas por toda la aplicación.

### Ejemplos

- Autenticación
- Interceptores HTTP
- Configuración global
- Guards
- Proveedores de aplicación
- Utilidades generales

La capa **core no debe contener lógica de negocio específica de dominios**.

---

# Capa Shared

shared/

Contiene elementos **reutilizables** sin lógica de negocio.

### Ejemplos

- Componentes UI reutilizables
- Directivas
- Pipes
- Funciones utilitarias
- Modelos comunes
- Elementos del sistema de diseño

Los elementos dentro de `shared` deben ser **agnósticos al dominio**.

---

# Capa Shell

shell/

Responsable de la **composición general de la aplicación**.

Incluye:

- Layout principal
- Navegación global
- Configuración de rutas principales
- Páginas base del sistema

Ejemplos:
shell/layouts
shell/navigation
shell.routes.ts

---

# Dominios

Toda la funcionalidad de negocio se encuentra dentro de:
domains/

Cada dominio representa un **bounded context** dentro del sistema.

### Dominios actuales

auth
catalogos
registro
mis-registros
solicitudes
validaciones
administracion
usuarios
reportes
notificaciones

Cada dominio sigue la misma arquitectura interna.

---

# Estructura Interna de un Dominio

nombre-dominio
├ application
├ domain
├ infrastructure
└ presentation

## application

Contiene la lógica de **orquestación de casos de uso**.

Ejemplos:

- Casos de uso
- Facades
- Manejo de estado
- Mapeadores
- Validadores

---

## domain

Contiene la **lógica de negocio pura**.

Ejemplos:

- Entidades
- Value Objects
- Reglas de negocio
- Interfaces de repositorios

La capa de dominio **no debe depender de Angular ni de frameworks externos**.

---

## infrastructure

Contiene **integraciones externas**.

Ejemplos:

- Clientes HTTP
- Adaptadores de API
- DTOs
- Implementaciones de repositorios

---

## presentation

Contiene los elementos de interfaz construidos con Angular.

Ejemplos:

- Pages
- Componentes
- Formularios
- Diálogos
- View Models

La capa de presentación debe comunicarse únicamente con **facades de la capa application**, nunca directamente con infraestructura.

---

# Estrategia de Rutas

El sistema de rutas está dividido en tres niveles.

## 1. Rutas de aplicación

app.routes.ts

Punto de entrada principal de la aplicación.

---

## 2. Rutas del Shell

shell.routes.ts

Define navegación principal y layouts globales.

---

## 3. Rutas por dominio

Cada dominio define sus propias rutas.

Ejemplo:
auth.routes.ts
registro.routes.ts
solicitudes.routes.ts

Esto permite **lazy loading y aislamiento entre dominios**.

---

# Flujo de Desarrollo

El desarrollo de funcionalidades debe seguir el siguiente orden:

1. Definir el **caso de uso del dominio**
2. Implementar la **lógica de aplicación**
3. Definir **entidades y reglas del dominio**
4. Implementar **adaptadores de infraestructura**
5. Construir **componentes de presentación**

Los componentes deben crearse **únicamente después de definir la lógica de negocio**.

---

# Estándares de Código

## Convención de nombres de archivos

kebab-case

Ejemplo:
registro-page.component.ts
crear-solicitud.use-case.ts
usuario.repository.ts

---

## Convención de tipos y clases

PascalCase

---

## Convención de variables

camelCase

---

# Estrategia de Imports

Evitar imports relativos profundos.

Preferir aliases cuando estén configurados:
@core
@shared
@domains
@shell

---

# Reglas para Componentes

Los componentes Angular deben cumplir las siguientes reglas:

- Contener únicamente lógica de **presentación**
- No incluir **reglas de negocio**
- No realizar **llamadas HTTP**
- Utilizar **facades o servicios de estado** para interactuar con la aplicación

---

# Propósito del Repositorio

Este repositorio se ha inicializado con la **estructura arquitectónica antes de implementar funcionalidades**.

Los componentes y la lógica del sistema se introducirán progresivamente conforme se definan los casos de uso.

Este enfoque garantiza que el código nuevo respete los límites arquitectónicos desde el inicio.

---

# Contribuciones

Antes de implementar una nueva funcionalidad:

1. Identificar el **dominio correspondiente**
2. Definir el **caso de uso**
3. Implementar respetando la arquitectura existente
4. Evitar dependencias entre dominios

Todo nuevo código debe respetar la estructura definida.

---

# Licencia

Este proyecto se mantiene para **fines de desarrollo interno**.
