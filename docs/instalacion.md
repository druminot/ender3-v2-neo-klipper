# Instalación

## Stack Completo (Docker)

### Ubicación

```
/opt/klipper-stack/
```

### Servicios

| Contenedor | Puerto | Imagen |
|------------|--------|--------|
| klipper | (interno) | mkuf/klipper |
| moonraker | 7125 | mkuf/moonraker |
| mainsail | 80 (via traefik) | mainsail-crew/mainsail |
| traefik | 80 | traefik |

### Inicio

```bash
cd /opt/klipper-stack
docker compose --profile mainsail up -d
```

## Firmware — Compilación

### Configuración `make menuconfig`

```
[*] Enable extra low-level configuration options
    Microcontroller: STMicroelectronics STM32F103
    Processor model: STM32F103
    Bootloader offset: 28KiB
    Communication: Serial (USART1 PA10/PA9)
    (NEW) Disable SWD at startup  ← CRÍTICO para GD32F303
```

### Compilar

```bash
cd /opt/klipper-stack
docker compose --profile tools run --rm tools make -C /klipper KCONFIG_CONFIG=/config/build.config
```

### Flashear

1. Copiar `out/klipper.bin` a tarjeta SD
2. Renombrar a `firmware.bin`
3. Insertar en impresora y encender
4. Esperar 10-20 segundos
5. Retirar SD (NO necesita renombrarse a `.cur`)

### Build Artifacts

- Último firmware: `/opt/klipper-stack/out/klipper.bin` (39748 bytes)
- SHA256: `20e47bdb3ecbd66b0806aa4de57a9121`
