# Impresora 3D — Resumen del Proyecto

## Estado Actual (Julio 2026)

- Klipper + Mainsail instalados via Docker en servidor `domotica-ia` (100.114.148.95)
- Impresora Ender-3 V2 Neo con placa **v4.2.2 (GD32F303)**, CR-Touch, CH340 serial
- **Z-Offset: 0** — funciona correctamente para esta máquina (CR-Touch montado al nivel de la boquilla)
- MCU conectado, todos los ejes funcionando
- Bed mesh calibrado (perfil `default`, 5×5, bicubic)
- Prints de prueba exitosos

### Próximos Pasos

- [ ] Calibración PID (hotend y cama)
- [ ] Pressure Advance
- [ ] Input Shaping (con ADXL345)
- [ ] Obico (detección de fallos con IA)
- [ ] Conectar a Home Assistant via Moonraker

### Enlaces Útiles

| Recurso | URL |
|---------|-----|
| Mainsail | http://100.114.148.95 |
| Moonraker API | http://100.114.148.95:7125 |
| Home Assistant | http://192.168.1.123:8123 |
