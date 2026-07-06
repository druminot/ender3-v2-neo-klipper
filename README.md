# Ender-3 V2 Neo — Klipper + Docker (prind)

Respaldo completo de la configuración de Klipper para Ender-3 V2 Neo
con placa v4.2.2 (GD32F303), CR-Touch, corriendo en Docker con el
stack [prind](https://github.com/mkuf/prind).

## Estructura

```
├── docs/                        # Documentación del proyecto
│   ├── resumen.md               # Estado actual y próximos pasos
│   ├── hardware.md              # Especificaciones y pines
│   ├── instalacion.md           # Compilación y flasheo
│   ├── configuracion.md         # printer.cfg y moonraker
│   ├── calibracion.md           # Calibraciones realizadas
│   ├── uso.md                   # Cómo usar la impresora
│   └── troubleshooting.md       # Solución de problemas
├── gcodes/
│   └── test_square.gcode        # G-code de prueba
├── opt/klipper-stack/
│   ├── config/                  # Configs de Klipper/Moonraker
│   │   ├── printer.cfg          # Config principal
│   │   ├── moonraker.conf       # API Moonraker
│   │   ├── build.config         # Build de firmware
│   │   └── ...
│   ├── docker-compose.yaml      # Stack Docker
│   ├── docker-compose.override.yaml
│   └── out/
│       ├── klipper.bin          # Firmware compilado (GD32F303)
│       └── klipper.dict
└── etc/udev/rules.d/
    └── 99-klipper.rules         # Udev rule para CH340
```

## Servidor

- **Host:** domotica-ia (100.114.148.95, Ubuntu 26.04 x86_64)
- **Stack:** Docker Compose con prind (klipper + moonraker + mainsail + traefik)
- **MCU:** STM32F103, Serial USART1 PA10/PA9 via CH340
- **Firmware:** `CONFIG_STM32F103GD_DISABLE_SWD=y` (requerido para GD32F303)

## Estado

- Klipper conectado y listo
- Z-Offset: 0 (CR-Touch montado al nivel de la boquilla)
- Bed mesh calibrado (perfil `default`)
- Prints de prueba exitosos
