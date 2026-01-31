# Prueba Técnica - Automation & AI Engineer (Sureti)

Este repositorio contiene la solución propuesta para el reto de automatización de filtrado de leads hipotecarios, utilizando n8n e Inteligencia Artificial.

## 📺 Video Explicativo
Aquí explico el problema, la solución y las decisiones tomadas (Time-to-market, Mocks, etc.):
[**Ver Video en YouTube**](https://youtu.be/znpN2g3hrwY)

## 📂 Contenido del Repositorio

1.  **Workflows (n8n):**
    * `workflows/1_lead_intake_process.json`: Flujo principal que recibe el lead, consulta mocks (Registraduría/SNR), ejecuta el Agente de IA para scoring y notifica.
    * `workflows/2_error_audit_template.json`: Sistema centralizado de manejo de errores que notifica a Slack y traduce logs técnicos con IA.
2.  **Documentación:**
    * `docs/politica_aceptacion.pdf`: Política de riesgo diseñada para el reto.
    * `docs/architecture_diagram.svg`: Vista gráfica del flujo de automatización.
3.  **Data Samples:**
    * `examples/`: Ejemplos JSON de entrada y salida para pruebas.

## 🏗️ Arquitectura de la Solución

El flujo sigue los siguientes pasos lógicos:

1.  **Ingesta:** Webhook recibe datos del formulario web.
2.  **Validación & Mocks:**
    * Simulación de consulta a Registraduría (Estado civil, vigencia cédula).
    * Simulación de consulta a SNR (Propiedad del inmueble, embargos, gravámenes).
3.  **Motor de Riesgo (AI Agent):**
    * Un agente de IA analiza los datos contra la *Política de Aceptación*.
    * Calcula LTV (Loan-to-Value) y asigna un puntaje (0-100).
    * Clasifica en: `NO_VIABLE`, `VIABLE`, o `ALTAMENTE_VIABLE`.
4.  **Persistencia & Notificación:**
    * Los datos se guardan en Google Sheets.
    * Se envía un correo automático al cliente con la decisión preliminar.
5.  **Manejo de Errores:**
    * Si el flujo falla, un workflow secundario captura el error, lo traduce a lenguaje natural y alerta al equipo técnico vía Slack.

## 🚀 Cómo usar estos Workflows

1.  Instalar [n8n](https://n8n.io/).
2.  Importar los archivos `.json` ubicados en la carpeta `workflows`.
3.  Configurar las credenciales necesarias (OpenAI, Google Sheets, Gmail, Slack).
4.  Ejecutar el webhook de prueba.

---
*Desarrollado para el proceso de selección de Sureti.*
