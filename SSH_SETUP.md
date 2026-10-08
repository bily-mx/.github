# Configuración SSH para GitHub

Esta guía describe la configuración estándar de SSH para developers de Profact en Windows.

## 1. Crear llave individual

```bash
ssh-keygen -t ed25519 -C "correo@profact.com"
```

Usar la ubicación propuesta por defecto:

```text
C:\Users\USUARIO\.ssh\id_ed25519
```

Se recomienda utilizar passphrase.

Se generan dos archivos:

```text
id_ed25519       llave privada
id_ed25519.pub   llave pública
```

La llave privada nunca debe compartirse ni registrarse en GitHub.

## 2. Habilitar ssh-agent

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

## 3. Usar Windows OpenSSH

Para estandarizar el cliente SSH utilizado por Git:

```bash
git config --global core.sshCommand "C:/Windows/System32/OpenSSH/ssh.exe"
```

## 4. Registrar la llave pública en GitHub

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

## 5. Validar conexión

```bash
ssh -T git@github.com
```

La autenticación debe completarse correctamente.

## 6. Clonar repositorios

Utilizar la URL SSH:

```bash
git clone git@github.com:ORGANIZACION/REPOSITORIO.git
```

Verificar el remoto:

```bash
git remote -v
```

Debe utilizar:

```text
git@github.com:
```

## 7. Consideraciones

- Cada persona utiliza una llave propia.
- No se comparten llaves privadas.
- Una llave comprometida debe eliminarse de GitHub y reemplazarse.
- Si cambia el equipo de trabajo, debe registrarse una llave nueva para ese equipo.
- HTTPS no forma parte del flujo estándar soportado por Profact.
