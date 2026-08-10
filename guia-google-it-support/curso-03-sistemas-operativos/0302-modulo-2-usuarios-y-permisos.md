# 0302 · Módulo 2: Usuarios y Permisos

> Curso 03 · Módulo 2 de 6 · Temas: cuentas, grupos, permisos, ACL, UAC y sudo

---

## Objetivos de este módulo

- [ ] Gestionar usuarios y grupos en Windows y Linux
- [ ] Entender los permisos de archivo (rwx) y su numeración
- [ ] Conocer ACL para permisos finos
- [ ] Explicar UAC (Windows) y sudo (Linux)

---

## 1. Usuarios y grupos

| Concepto | Windows | Linux |
|----------|---------|-------|
| Usuario | Cuenta local o de dominio | `/etc/passwd` |
| Grupo | Grupos locales/del dominio | `/etc/group` |
| Crear usuario | `net user nombre clave /add` | `sudo useradd -m nombre` |
| Ver grupos | `net localgroup` | `groups usuario`, `id` |
| "Soy admin" | Grupo `Administrators` | Grupo `sudo` |

**Reglas de gestión**:
- Crea una cuenta por persona (nunca compartas cuentas).
- **Mínimo privilegio**: solo lo necesario, solo cuando es necesario.
- Contraseñas: 12+ caracteres, únicas; activa 2FA donde se pueda; usa gestor de contraseñas.
- **Desaprovisionamiento**: al despedir/salir, desactiva la cuenta y audita accesos.

---

## 2. Permisos en Linux (rwx)

Cada archivo/carpeta tiene dueño (user), grupo (group) y otros (others), con permisos de **r**ead (leer), **w**rite (escribir), e**x**ecute (ejecutar).

| Número | Permiso | Letras |
|--------|---------|--------|
| 4 | leer | r-- |
| 5 | leer + ejecutar | r-x |
| 6 | leer + escribir | rw- |
| 7 | todo | rwx |

**`chmod 754`** = dueño rwx (7) · grupo r-x (5) · otros r-- (4).

```bash
chmod 755 script.sh    # típico para scripts ejecutables
chown usuario:grupo archivo   # cambiar dueño
sudo chown -R $USER:$USER /home/usuario
```

Ver permisos: `ls -l` → `-rwxr-xr-- 1 diego diego 1024 mar 1 file`.

**`umask 022`**: los archivos nuevos se crean con permisos restringidos por defecto (seguridad).

---

## 3. ACL (permisos granulares)

Cuando rwx no basta (ej. dar acceso a "solo revisión" a un tercero):
```bash
setfacl -m u:contador:r /home/soporte/ventas   # dar lectura a un usuario
setfacl -x u:contador /home/soporte/ventas      # quitar
getfacl /home/soporte/ventas                    # ver ACL
```
Windows equivalente: pestaña **Seguridad → Avanzado** en las propiedades del archivo (ACL de NTFS).

---

## 4. Control de acceso en Windows

| Herramienta | Función |
|-------------|---------|
| **NTFS permissions** | Permisos por archivo/carpeta (Leer, Escritura, Control total) |
| **UAC (Control de Cuentas)** | Ventana "¿Permites que esta aplicación haga cambios?" — primer firewall contra malware que quiere ser admin |
| **Credenciales/Protected Storage** | Gestor de credenciales de Windows |
| **`icacls`** | Command line para ACLs de NTFS |

> **Explicación de usuario**: UAC es como pedirle permiso al portero cada vez que una aplicación quiere entrar con llave maestra. Si no la reconoces, dices NO.

---

## 5. Escenarios de soporte con usuarios

| Síntoma | Diagnóstico clásico |
|---------|---------------------|
| "No puedo instalar programas" | Cuenta sin privilegios de admin → ¿debería tenerlos? (si no: solución correcta) |
| "Acceso denegado a una carpeta" | Permisos NTFS/ext4/ACL → revisar `ls -l`/Seguridad avanzada |
| "No encuentro mis documentos" | Perfil dañado o movido → revisar `%UserProfile%` / `/home` |
| Usuario despedido con acceso | **Inmediato**: desactivar cuenta de dominio/local + revocar grupos |

---

## Práctica del módulo

1. Linux (VM): crea 2 usuarios, un grupo `soporte`, pon a ambos en el grupo; crea un archivo con `chmod 640` y otro `754`; observa con `ls -l`.
2. Windows: revisa los permisos NTFS de `C:\Users\Público` (Seguridad → Avanzado).
3. Practica `setfacl`/`getfacl` (Linux) para un permiso especial.
4. Identifica en tu Windows si UAC está activo (Panel de control → Cuentas).

## Plataformas gratuitas para practicar

- **Linux Journey — Permissions** (https://linuxjourney.com)
- **OverTheWire Bandit** niveles con `chmod`
- **TryHackMe — Linux Fundamentals rooms** (https://tryhackme.com)

---

## Checklist de dominio — Módulo 2

- [ ] Creo y gestiono usuarios y grupos en ambos SO desde la CLI
- [ ] Calculo `chmod` de memoria (4/2/1)
- [ ] Explico mínima exclusión, mínimo privilegio y UAC con ejemplos
- [ ] Doy permisos especiales con ACL y los audito
- [ ] Resuelvo "acceso denegado" diagnosticando permisos
- [ ] Aplico desaprovisionamiento inmediato cuando se requiere