# FinVox 🎙️💳

FinVox es una plataforma bancaria de voz de baja latencia que combina una interfaz conversacional fluida con una **capa pasiva de telemetría y biometría vocal** para detectar ataques de ingeniería social, *vishing* y clonación de voz por Inteligencia Artificial (*deepfakes*) en tiempo real.

---

## 🌟 Características Principales

- **Atención Vocal en Tiempo Real:** Conversación bidireccional continua de ultra baja latencia utilizando streaming de audio sobre WebSockets.
- **Biometría Vocal y Telemetría Pasiva:** Análisis fisiológico y conductual en segundo plano sin interrupción de la experiencia del usuario.
- **Detección Anti-Deepfake (DSP):** Extracción de espectrogramas por Transformada Rápida de Fourier (FFT), entropía espectral y análisis de formantes para detectar síntesis de voz no humana.
- **Matriz Dinámica de Riesgo:** Motor de Scoring que ejecuta decisiones automáticas en tiempo real:
  - `ALLOW` (< 35% riesgo): Transacción aprobada sin fricción.
  - `STEP_UP_AUTH` (35% - 70% riesgo): Requerimiento de segundo factor (Push / Biometría Facial).
  - `BLOCK_AND_ESCALATE` (> 70% riesgo): Bloqueo inmediato y transferencia a operador de fraude.

---

## 🏗️ Arquitectura del Sistema

```text
       [ Cliente / React + Vite ]
                   │
           (Audio Stream / PCM)
                   │
                   ▼
     ┌───────────────────────────┐
     │   Backend Proxy / FastAPI │
     └─────────────┬─────────────┘
                   │
         ┌─────────┴─────────┐
         ▼                   ▼
┌─────────────────┐ ┌──────────────────┐
│ Engine de Voz   │ │ Telemetry Engine │
│ (Gemini Live)   │ │ (DSP + Anti-Fake)│
└─────────────────┘ └──────────────────┘
