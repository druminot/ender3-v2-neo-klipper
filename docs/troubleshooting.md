# Troubleshooting

## MCU Shutdown

```
Can not update MCU 'mcu' config as it is shutdown
```

**Causa:** La impresora se apagó/desconectó o hubo un error de firmware.

**Solución:**
```bash
# Power cycle la impresora (desconectar y conectar USB)
# Luego:
docker exec klipper-stack-moonraker-1 \
  curl -s -X POST "http://localhost:7125/printer/firmware_restart"
```

## SD Card No Renombra firmware.bin

Es **normal** en placas GD32F303. El flasheo fue exitoso si:
- Klipper se conecta al MCU (`state: ready`)
- Puedes hacer G28 sin errores

No confiar en `firmware.cur`.

## Z-Offset Incorrecto

Síntomas:
- Nozzle arrastra contra la cama (z_offset muy positivo o mal signo)
- Material no se adhiere (z_offset muy negativo o cero)
- Boquilla se ensucia después de prints largos

**Solución:** Recalibrar con `PROBE_CALIBRATE` + papel.

Recordatorio: en Klipper el z_offset es **positivo** (al revés que Marlin).

## Pantalla en Blanco

Normal. La pantalla DWIN T5L7B no es compatible con Klipper. Usar Mainsail (web UI).

## Error Serial

```
mcu 'mcu': Unable to connect
```

**Causas:** CH340 desconectado, permiso denegado, o udev rule incorrecta.

**Verificar:**
```bash
ls -la /dev/klipper
ls -la /dev/ttyUSB0
cat /etc/udev/rules.d/99-klipper.rules
```

**Reconectar:**
```bash
# Power cycle impresora
docker restart klipper-stack-klipper-1
```

## G-Code No Se Encuentra

Los archivos se almacenan en `/opt/printer_data/gcodes/` dentro del contenedor moonraker, no en el host.

Para subir desde línea de comandos:
```bash
docker exec -i klipper-stack-moonraker-1 \
  sh -c 'cat > /opt/printer_data/gcodes/archivo.gcode' < ./local.gcode
```

## Debugging

```bash
# Ver logs de Klipper
docker logs klipper-stack-klipper-1

# Ver logs de Moonraker
docker logs klipper-stack-moonraker-1

# Consultar estado
docker exec klipper-stack-moonraker-1 \
  curl -s "http://localhost:7125/printer/objects/query?print_stats"
```
