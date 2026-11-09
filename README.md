# OpenPdM AC Motors

**Framework open-source de monitoreo predictivo industrial mediante Edge AI**

Trabajo Final de Maestría en Robótica e Inteligencia Artificial (PRIA) — Universidad Tecnológica (UTEC), Uruguay
Autor: Juan Pedro de León Sum

> **English summary.** Open-source, distributed condition-based monitoring framework for three-phase induction motors, built on Edge AI. It extends a 2020 LSTM proof of concept (published at IEEE URUCON 2026, see [`legacy/2020-poc/`](legacy/2020-poc/)) toward an operational deployment in an agro-industrial plant with more than 100 motors. Work in progress.

## Descripción

Sistema distribuido de código abierto para el monitoreo basado en condición (CBM) de motores de inducción trifásicos. El objetivo es su despliegue y validación en una planta agroindustrial uruguaya con más de 100 motores en operación continua.

El proyecto propone una arquitectura jerárquica de IA en tres niveles:

| Nivel | Modelo | Plataforma | Función |
|---|---|---|---|
| 1. Borde | TCN (*Temporal Convolutional Networks*) cuantizadas | Nodos ESP32-S3 con ADXL355 (vibración) y DS18B20 (temperatura) | Detección de anomalías en tiempo real |
| 2. Servidor | TFT (*Temporal Fusion Transformers*) | Servidor centralizado | Pronóstico multivariable de vida útil remanente (RUL) con horizonte de 24 h |
| 3. Planta | GNN (*Graph Neural Networks*) | Servidor centralizado | Modelado de la propagación de vibraciones entre motores adyacentes, para reducir falsos positivos por contaminación cruzada |

La severidad de vibración se evalúa con referencia a ISO 20816-1:2016.

## Antecedentes

Este trabajo continúa directamente el Trabajo Final de Especialización del autor: un prototipo de 2020 basado en ESP8266, MPU-6050 y una red LSTM, validado en laboratorio (TRL 4).

- Artículo: J. P. de León Sum y E. M. Gonçalves, "Open-Source Predictive Maintenance System for AC Induction Motors Using LSTM Neural Networks and Low-Cost Embedded Hardware", *IEEE URUCON 2026*.
- Tesis original: [10.5281/zenodo.21135685](https://doi.org/10.5281/zenodo.21135685)
- Materiales del prototipo: [`legacy/2020-poc/`](legacy/2020-poc/)

Las limitaciones identificadas en ese prototipo orientan el diseño actual:

| Limitación del prototipo 2020 | Respuesta en este trabajo |
|---|---|
| Banda de 10 Hz a 260 Hz (MPU-6050) | ADXL355, banda completa de 10 Hz a 1 000 Hz |
| Sensor montado cerca de las patas del motor | Montaje sobre los alojamientos de rodamiento |
| Conversión heurística de aceleración a mm/s | Pronóstico directo de velocidad de vibración, validado contra un vibrómetro de referencia |
| Sin líneas base y una sola corrida por configuración | Comparación con persistencia, regresión lineal y ARIMA, con varias semillas |
| Validación en laboratorio con dos motores | Despliegue en planta, objetivo TRL 7 |

## Estado actual

🚧 **En desarrollo**

- [x] Capítulos de Introducción, Objetivos y Estado del Arte redactados
- [ ] Diseño de hardware (PCB en KiCad) — en curso
- [ ] Firmware del nodo (ESP-IDF + FreeRTOS)
- [ ] Modelos TCN, TFT y GNN
- [ ] Despliegue y validación en planta

## Estructura del repositorio

| Ruta | Contenido |
|---|---|
| `main.tex`, `Biblio.bib` | Documento de tesis (LaTeX) |
| `hardware/` | Diseño de PCB (KiCad) y lista de materiales |
| `firmware/` | Firmware ESP-IDF + FreeRTOS para ESP32-S3 |
| `models/` | Modelos TCN, TFT y GNN (PyTorch) |
| `legacy/2020-poc/` | Prototipo de 2020 citado en el artículo de URUCON 2026 |

## Cómo citar

Para el prototipo de 2020 y sus resultados, citá el artículo de IEEE URUCON 2026 (ver [`legacy/2020-poc/CITATION.cff`](legacy/2020-poc/CITATION.cff)). La forma de citar este trabajo se agregará cuando haya resultados publicados.

## Licencia

Código abierto bajo licencia [MIT](LICENSE).
