# Onboarding de GitHub para Profact

Este documento describe los pasos que debe completar cualquier colaborador antes de trabajar en repositorios de Profact.

## 1. Cuenta personal de GitHub

Cada colaborador debe utilizar una cuenta individual de GitHub.

No se utilizan cuentas compartidas.

Si el colaborador no tiene una cuenta, debe crearla antes de solicitar acceso.

## 2. Agregar y verificar el correo corporativo

Agregar el correo corporativo de Profact a la cuenta personal de GitHub:

```text
GitHub
→ Settings
→ Emails
→ Add email address
```

Agregar:

```text
usuario@profact.com.mx
```

y completar la verificación.

El correo corporativo no necesita ser el correo principal de la cuenta, pero sí debe estar agregado y verificado.

## 3. Solicitar acceso

Enviar un correo a la administración TI:

```text
andres@profact.com.mx
```

Asunto sugerido:

```text
Solicitud de acceso a GitHub Profact
```

Contenido mínimo:

```text
Nombre completo:
Usuario de GitHub:
Repositorio(s) o proyecto(s) requeridos:
```

El usuario de GitHub debe incluirse aunque el correo corporativo ya esté verificado. Esto evita ambigüedades y permite confirmar que la invitación se envía a la cuenta correcta.

## 4. Configurar identidad Git

En cada repositorio de Profact:

```bash
git config user.name "Nombre Apellido"
git config user.email "usuario@profact.com.mx"
```

Se recomienda configurarlo a nivel de repositorio y no globalmente si el equipo también se utiliza para proyectos personales.

Verificar:

```bash
git config user.name
git config user.email
```

El correo utilizado en commits debe coincidir con el correo corporativo agregado y verificado en GitHub.

## 5. Crear una llave SSH

Cada developer utiliza su propia llave SSH:

```bash
ssh-keygen -t ed25519 -C "usuario@profact.com.mx"
```

El valor de `-C` es únicamente una etiqueta.

Usar la ubicación propuesta por defecto:

```text
C:\Users\USUARIO\.ssh\id_ed25519
```

Se recomienda utilizar passphrase.

Se generan:

```text
id_ed25519       llave privada
id_ed25519.pub   llave pública
```

La llave privada nunca debe compartirse ni enviarse a Profact.

## 6. Habilitar ssh-agent en Windows

Abrir PowerShell como administrador:

```powershell
Set-Service -Name ssh-agent -StartupType Automatic
Start-Service ssh-agent
```

Después, en una terminal normal:

```powershell
ssh-add $env:USERPROFILE\.ssh\id_ed25519
```

Verificar:

```powershell
ssh-add -l
```

## 7. Configurar Git para usar Windows OpenSSH

```bash
git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"
```

## 8. Registrar la llave pública en GitHub

Copiar el contenido de:

```text
C:\Users\USUARIO\.ssh\id_ed25519.pub
```

En GitHub:

```text
Settings
→ SSH and GPG keys
→ New SSH key
```

Registrar únicamente la llave pública.

Profact no necesita ni debe recibir la llave privada.

## 9. Validar la conexión

```bash
ssh -T git@github.com
```

La autenticación debe completarse correctamente.

## 10. Clonar repositorios

Utilizar la URL SSH:

```bash
git clone git@github.com:ORGANIZACION/REPOSITORIO.git
```

Verificar:

```bash
git remote -v
```

El remoto debe utilizar:

```text
git@github.com:
```

HTTPS no forma parte del flujo estándar soportado por Profact.

## 11. Acceso y llaves

El acceso funciona mediante:

```text
Cuenta GitHub del colaborador
        ↓
Permiso dentro de la organización/repositorio
        ↓
Llave SSH registrada en esa cuenta
```

Profact administra permisos. Cada colaborador administra sus propias llaves y dispositivos.

Una llave comprometida debe eliminarse inmediatamente de GitHub y reemplazarse.

## 12. Checklist

- [ ] Cuenta personal de GitHub creada.
- [ ] Correo corporativo agregado y verificado.
- [ ] Acceso solicitado.
- [ ] Invitación aceptada.
- [ ] `user.name` configurado.
- [ ] `user.email` corporativo configurado.
- [ ] Llave SSH individual creada.
- [ ] Llave pública registrada en GitHub.
- [ ] `ssh-agent` configurado.
- [ ] Conexión SSH validada.
- [ ] Repositorio clonado mediante SSH.
