# Hardware

## Impresora

| Especificación | Valor |
|---------------|-------|
| Modelo | Creality Ender-3 V2 Neo |
| Board | v4.2.2 (GD32F303, no STM32) |
| Probe | CR-Touch (BLTouch clone) |
| Hotend | Stock V2 Neo |
| Cama | Aluminio + plataforma magnética |
| Extrusor | Bowden stock |
| Nozzle | 0.4mm |
| Pantalla | DWIN T5L7B (no compatible con Klipper) |

## Placa v4.2.2 — Pines MCU (GD32F303)

| MCU Pin | Función |
|---------|---------|
| PA0 | Ventilador de capa |
| PA1 | Calentador del hotend |
| PA2 | Calentador de la cama |
| PA5 | Endstop X |
| PA6 | Endstop Y |
| PB0 | Control CR-Touch (servo) |
| PB1 | Sensor CR-Touch |
| PB3 | Paso extrusor (dir) |
| PB4 | Paso extrusor (step) |
| PB5 | Paso Z (dir) |
| PB6 | Paso Z (step) |
| PB7 | Paso Y (dir) |
| PB8 | Paso Y (step) |
| PB9 | Paso X (dir) |
| PB13 | Beeper |
| PC2 | Paso X (step) |
| PC3 | Enable de motores |
| PC4 | Sensor cama (termistor) |
| PC5 | Sensor hotend (termistor) |

## CH340 — Conexión USB

- Serial USART1 en PA10 (TX) / PA9 (RX) via CH340 USB
- `/dev/ttyUSB0` → symlink `/dev/klipper`
- udev rule en `/etc/udev/rules.d/99-klipper.rules`

## Placa GD32F303 — Particularidades

- NO renombra `firmware.bin` a `firmware.cur` tras flasheo exitoso
- La presencia de `firmware.cur` **no** es indicador confiable de flasheo
- Requiere `CONFIG_STM32F103GD_DISABLE_SWD=y` en la compilación
