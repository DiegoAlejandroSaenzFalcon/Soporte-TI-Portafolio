# 0202 Â· MÃ³dulo 2: Capa de Red â€” IP y Subredes

> Curso 02 Â· MÃ³dulo 2 de 6 Â· Temas: IPv4, IPv6, mÃ¡scaras, CIDR, subredes y enrutamiento

---

## Objetivos de este mÃ³dulo

- [ ] Leer y explicar una direcciÃ³n IPv4 y su mÃ¡scara
- [ ] Calcular subredes y hosts por subred
- [ ] Entender CIDR y el direccionamiento sin clases
- [ ] Explicar cÃ³mo funciona el enrutamiento entre redes
- [ ] Conocer el formato bÃ¡sico de IPv6

---

## 1. La direcciÃ³n IP (IPv4)

32 bits agrupados en 4 octetos: `192.168.1.50` = `11000000.10101000.00000001.00110010`

Dos partes: **red** (quiÃ©n eres de dÃ³nde) + **host** (cuÃ¡l eres). La **mÃ¡scara de subred** delimita dÃ³nde termina cada parte.

| MÃ¡scara | CIDR | Hosts Ãºtiles |
|---------|------|--------------|
| 255.255.255.0 | /24 | 254 |
| 255.255.255.128 | /25 | 126 |
| 255.255.255.192 | /26 | 62 |
| 255.255.0.0 | /16 | 65 534 |
| 255.0.0.0 | /8 | 16 777 214 |

**FÃ³rmula de hosts**: `2^(32 - CIDR) - 2` (restamos red y broadcast). Ej: /24 â†’ 2^8 - 2 = 254.

**Reglas importantes**:
- La primera IP de cada subred = **direcciÃ³n de red** (no usable).
- La Ãºltima IP = **broadcast** (envÃ­os a todos, no usable).
- Rango privado (nunca sale a Internet): **10.x.x.x**, **172.16â€“31.x.x**, **192.168.x.x**.
- **127.0.0.1** = loopback ("yo mismo"); el alias `localhost`.

---

## 2. Subnetting en la prÃ¡ctica

Â¿Por quÃ© subdividir? Para **separar redes** (seguridad, trÃ¡fico, organizaciÃ³n) sin desperdiciar IPs.

![Subnetting visual](./diagramas/subredes.svg)

**Ejemplo guiado**: la red 192.168.1.0/24 la necesitas en 4 subredes.
1. 4 subredes â†’ necesitas 2 bits (`2^2 = 4`) â†’ mÃ¡scara /26 (255.255.255.192).
2. Cada subred tiene `2^6 - 2 = 62` hosts.
3. Tabla de resultados:

| Subred | Rango | Broadcast |
|--------|-------|-----------|
| 192.168.1.0/26 | .1 â€“ .62 | .63 |
| 192.168.1.64/26 | .65 â€“ .126 | .127 |
| 192.168.1.128/26 | .129 â€“ .190 | .191 |
| 192.168.1.192/26 | .193 â€“ .254 | .255 |

> **Truco mental**: la "magia" de la subred = la cantidad de la mÃ¡scara no estÃ¡ndar (192 â†’ paso de 64 IPs).

---

## 3. Enrutamiento (cÃ³mo viajan los datos entre redes)

```mermaid
flowchart LR
    A[PC - 192.168.1.50\nred local] -->|trama hacia el gateway| R[Router A\n192.168.1.1]
    R -->|siguiente salto| R2[Router B\npor tabla de rutas]
    R2 -->|desencapsula y entrega| D[Servidor - 10.20.3.8\nred remota]
```

| Concepto | DefiniciÃ³n |
|----------|------------|
| **Ruta (route)** | "Para llegar a la red X, envÃ­a al host Y" |
| **Tabla de rutas** | El mapa del router (destino â†’ siguiente salto) |
| **Gateway** | El router de salida de tu subred |
| **Ruta estÃ¡tica** | Configurada a mano |
| **Ruta dinÃ¡mica** | Protocolos (OSPF, BGP, RIP) que aprenden automÃ¡ticamente |
| **InterconexiÃ³n (interfaces)** | Cada red conectada al router tiene su propia IP en ese segmento |

**CÃ³mo decide un router**: para cada paquete busca en su tabla la ruta de **mayor coincidencia** (la mÃ¡s especÃ­fica) hacia el destino.

---

## 4. IPv6 (el futuro ya presente)

- **128 bits**, 8 grupos hexadecimales: `2606:4700:4700::1111`
- No hay escasez: miles de millones de direcciones por persona.
- **NotaciÃ³n `::`** comprime grupos de ceros (solo una vez).
- Los equipos actuales usan IPv4 + IPv6 a la vez (**doble pila**).
- `ping ::1` = loopback IPv6. `nslookup`/`dig` muestran registros AAAA.

---

## PrÃ¡ctica del mÃ³dulo (clave: hacer muchas subredes a mano)

1. Calcula: Â¿cuÃ¡ntas subredes de /28 salen de una /24? (16) Â¿CuÃ¡ntos hosts por subred? (14)
2. Dada 172.16.0.0/16, divide en 8 subredes: escribe los 8 rangos. Usa subnettingpractice.com para verificar.
3. En Packet Tracer: conecta 3 redes con 2 routers, configura IPs estÃ¡ticas y verifica con `ping` PCâ†’servidor remoto.

## Plataformas gratuitas para practicar

- **subnettingpractice.com** â€” entrenador infinito de mÃ¡scaras/subredes
- **Packet Tracer** (NetAcad) â€” laboratorios de enrutamiento entre routers
- **Quizlet** en la web: busca *"IPv4 subnetting practice questions"*
- Curso gratuito *"CCNA: Introduction to Networks"* en NetAcad (nivel avanzado, opcional)

---

## Checklist de dominio â€” MÃ³dulo 2

- [ ] Explico quÃ© parte de la IP corresponde a red y cuÃ¡l a host
- [ ] Calculo a mano hosts por subred (2^n - 2)
- [ ] Subdivido una red /24 en 2, 4, 8 o 16 subredes correctamente
- [ ] Identifico direcciÃ³n de red y broadcast de cualquier rango
- [ ] PillÃ© la idea de ruta/tabla/gateway y siguiente salto
- [ ] Reconozco una direcciÃ³n IPv6 y su loopback ::1

