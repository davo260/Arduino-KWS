# ArduinoKWS — Edge Impulse

Reconocimiento de palabras clave (Keyword Spotting) en español sobre board,  Arduino Nano 33 BLE Sense, con tres clases: `si`, `no`, `silencio`. Desplegado con Edge Impulse EON™ Compiler (RAM optimized).

## Resultados (validation set)

| Métrica | Valor |
|---|---|
| Accuracy | 98.3% |
| Loss | 0.10 |
| Area under ROC Curve | 1.00 |
| Weighted avg Precision | 0.98 |
| Weighted avg Recall | 0.98 |
| Weighted avg F1 score | 0.98 |

**F1 por clase**

| Clase | F1 |
|---|---|
| No | 0.97 |
| Si | 1.00 |
| Silencio | 0.98 |

**Confusion matrix**

| | No | Si | Silencio |
|---|---|---|---|
| **No** | 93.8% | 0% | 6.3% |
| **Si** | 0% | 100% | 0% |
| **Silencio** | 0% | 0% | 100% |

La única confusión notable es "no" clasificado como "silencio" en 6.3% de los casos; "si" y "silencio" no presentan errores en el set de validación.

## On-device performance (EON Compiler, quantized int8, RAM optimized)

| Métrica | Valor |
|---|---|
| Inferencing time | 4 ms |
| Peak RAM usage | 12.5 KB |
| Flash usage | 45.8 KB |

## Estructura del repo

```
.
├── README.md
├── deployment/       # Arduino library exportada desde Edge Impulse
├── scripts/          # scripts/notebooks de preprocesamiento o adquisición de datos
└── docs/             # capturas del dashboard, notas de diseño del impulse
```

## Uso

1. Abrir Arduino IDE.
2. `Sketch → Include Library → Add .ZIP Library` → seleccionar el `.zip` en `deployment/`.
3. Abrir el ejemplo incluido (`File → Examples → ArduinoKWS_inferencing → ...`).
4. Compilar y subir a la board.

## Notas

- Modelo cuantizado a int8, optimizado para uso de RAM.
- Frecuencia de muestro 44.1kHz
- Data set split 78%/22%
- Caracteristica "si"  - 1:05 minutos de data
- Caracteristica "no"  - 1:09 minutos de data
- Caracteristica "silencio"  - 1:20 minutos de data
