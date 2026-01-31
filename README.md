# Prueba Técnica - Automation & AI Engineer (Sureti)

Este repositorio contiene la solución propuesta para el reto de automatización de filtrado de leads hipotecarios, utilizando **n8n** e **Inteligencia Artificial**.

## 📺 Video Explicativo
Aquí explico el problema, la solución y las decisiones tomadas (Time-to-market, Mocks, decisiones de arquitectura):
[**Ver Video en YouTube**](https://youtu.be/znpN2g3hrwY)

## 📂 Contenido del Repositorio

A continuación se describen los archivos incluidos en este repositorio:

### 1. Workflows de Automatización (n8n)
* **[Sureti - Lead Intake Form (Template).json](./Sureti%20-%20Lead%20Intake%20Form%20(Template).json)**
    * *Flujo Principal:* Recibe el lead desde el formulario, consulta los mocks (Registraduría/SNR), ejecuta el Agente de IA para el scoring de riesgo y notifica el resultado.
* **[🚨 Template - Auditoría Errores con IA.json](./🚨%20Template%20-%20Auditoría%20Errores%20con%20IA.json)**
    * *Sistema de Auditoría:* Workflow centralizado que captura errores de otros flujos, utiliza IA para "traducir" el error técnico a lenguaje natural y notifica al equipo vía Slack.

### 2. Documentación y Diseño
* **[POLITICA-ACEPTACION.pdf](./POLITICA-ACEPTACION.pdf)**
    * Documento detallado con la política de riesgos, criterios de exclusión y sistema de puntaje (Scoring) diseñado para el reto.
* **[CAPTURE.svg](./CAPTURE.svg)**
    * Diagrama visual de la arquitectura del flujo de automatización.

## 🏗️ Arquitectura de la Solución

El flujo sigue los siguientes pasos lógicos:

1.  **Ingesta:** Webhook recibe datos estructurados del formulario web.
2.  **Validación & Mocks:**
    * Simulación de consulta a Registraduría (Estado civil, vigencia cédula).
    * Simulación de consulta a SNR (Propiedad del inmueble, embargos, gravámenes).
3.  **Motor de Riesgo (AI Agent):**
    * Un agente de IA analiza los datos cruzándolos con la *Política de Aceptación*.
    * Calcula métricas como el LTV (Loan-to-Value) y asigna un puntaje (0-100).
    * Clasifica el lead en: `NO_VIABLE`, `VIABLE`, o `ALTAMENTE_VIABLE`.
4.  **Persistencia & Notificación:**
    * Los datos procesados se guardan en Google Sheets.
    * Se envía un correo automático al cliente con la decisión preliminar.
5.  **Manejo de Errores:**
    * Si el flujo falla, el workflow de auditoría captura el evento, lo traduce y alerta en tiempo real.

## 🚀 Cómo usar estos Workflows

1.  Tener una instancia de [n8n](https://n8n.io/) activa.
2.  Descargar los archivos `.json` de este repositorio.
3.  Importarlos en n8n ("Import from File").
4.  Configurar las credenciales necesarias (OpenAI, Google Sheets, Gmail, Slack).
5.  Activar el webhook de prueba.

---
*Desarrollado por Ivan Barros para el proceso de selección de Sureti.*
