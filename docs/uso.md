# Cómo Usar

## Web UI (Mainsail)

URL: **http://100.114.148.95**

- Dashboard: estado en tiempo real, temperaturas
- Control: mover ejes, home, extrude
- Console: terminal de G-Code
- Files: subir y gestionar G-Codes
- Print: historial de impresiones

## API Moonraker

Todas las requests van a `http://100.114.148.95:7125` (solo desde el servidor).

### Desde el Servidor

```bash
# Home
docker exec klipper-stack-moonraker-1 \
  curl -s -X POST "http://localhost:7125/printer/gcode/script" \
  -d "script=G28"

# Estado de objetos
docker exec klipper-stack-moonraker-1 \
  curl -s "http://localhost:7125/printer/objects/query?toolhead&extruder"

# Subir G-Code
docker exec -i klipper-stack-moonraker-1 \
  sh -c 'cat > /opt/printer_data/gcodes/mi_archivo.gcode' < ./local_file.gcode
```

### Desde Home Assistant (192.168.1.123)

- Integración: Moonraker
- URL: `http://192.168.1.123:7125`
- Muestra: temperaturas, estado, progreso

## Subir y Empezar un Print

1. Abrir http://100.114.148.95
2. Ir a Files → Upload
3. Seleccionar archivo `.gcode`
4. Click en el archivo → "Print"
5. O en Terminal: `START_PRINT BED_TEMP=60 EXTRUDER_TEMP=200`

El G-code de inicio debe incluir:

```
G28
BED_MESH_PROFILE LOAD=default
```

## Obico (Detección de Fallos con IA)

- Open-source, self-hosteable
- https://github.com/TheSpaghettiDetective/moonraker-obico
- Requiere cámara web apuntando a la impresora
- Plan gratuito: 1 impresora

Alternativa: OctoEverywhere (más generoso, no self-hosteable)
