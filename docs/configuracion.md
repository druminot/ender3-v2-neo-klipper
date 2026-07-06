# Configuración

## Archivos

| Archivo | Ruta |
|---------|------|
| Config principal | `/opt/klipper-stack/config/printer.cfg` |
| Moonraker | `/opt/klipper-stack/config/moonraker.conf` |
| Build config | `/opt/klipper-stack/config/build.config` |
| Datos de impresión | `/opt/printer_data/gcodes/` |
| Firmware | `/opt/klipper-stack/out/klipper.bin` |

## printer.cfg — Secciones Clave

### MCU

```ini
[mcu]
serial: /dev/klipper
restart_method: command
```

### BLTouch / CR-Touch

```ini
[bltouch]
sensor_pin: ^PB1
control_pin: PB0
x_offset: -45.0
y_offset: -10.0
z_offset: 0
speed: 20
samples: 1
sample_retract_dist: 8.0
```

> `z_offset = 0` es correcto para Ender-3 V2 Neo. El CR-Touch está montado al mismo nivel que la boquilla.
> `x_offset` / `y_offset` calibrados para el soporte stock del V2 Neo.

### Safe Z Home

```ini
[safe_z_home]
home_xy_position: 160,120
```

> Sin `z_hop` — usa valores por defecto.

### Bed Mesh

```ini
[bed_mesh]
speed: 120
horizontal_move_z: 8
mesh_min: 30, 30
mesh_max: 189, 189
probe_count: 5, 5
algorithm: bicubic
fade_start: 1
fade_end: 10
fade_target: 0
```

## G-Code de Inicio (Slicer)

```
G28 ; Home
BED_MESH_PROFILE LOAD=default
G1 Z5 F3000
```

## Moonraker

- Host: `0.0.0.0`
- Puerto: `7125`
- Trusted IPs: LAN completa (192.168.x.x)
- CORS habilitado
