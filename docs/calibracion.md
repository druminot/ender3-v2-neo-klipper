# Calibraciones Realizadas

## ✅ Bed Mesh — COMPLETADO

- Grilla 5×5 en 4 knots bicúbicos
- Variación ≈ 0.46mm
- Perfil guardado como `default`
- Se carga automáticamente con `BED_MESH_PROFILE LOAD=default`

## ✅ Z-Offset — COMPLETADO

Valor: `z_offset = 0`

El CR-Touch del Ender-3 V2 Neo está montado al mismo nivel que la boquilla. Cuando el pin toca la cama, la boquilla está a ~0mm de la cama.

### Verificación

```bash
docker exec klipper-stack-moonraker-1 \
  curl -s -X POST "http://localhost:7125/printer/gcode/script" \
  -d "script=G28"
docker exec klipper-stack-moonraker-1 \
  curl -s -X POST "http://localhost:7125/printer/gcode/script" \
  -d "script=PROBE"
```

El resultado debe ser `z≈0`.

### Si Necesitas Recalibrar

1. `G28` (home)
2. `PROBE_CALIBRATE` (inicia wizard)
3. Desliza papel entre nozzle y cama
4. Usa `TESTZ Z=-0.1` / `TESTZ Z=+0.1` hasta sentir roce
5. `ACCEPT` → `SAVE_CONFIG`

## ❌ PID — PENDIENTE

Calentar hotend a 200°C y cama a 60°C, luego:

```bash
PID_CALIBRATE HEATER=extruder TARGET=200
PID_CALIBRATE HEATER=heater_bed TARGET=60
SAVE_CONFIG
```

## ❌ Pressure Advance — PENDIENTE

```bash
TUNING_TOWER COMMAND=SET_PRESSURE_ADVANCE PARAMETER=ADVANCE START=0 FACTOR=.005
```

## ❌ Input Shaper — PENDIENTE

Requiere ADXL345 conectado a Raspberry Pi.

## ❌ Screws Tilt Adjust — PENDIENTE

```bash
SCREWS_TILT_CALCULATE
```
