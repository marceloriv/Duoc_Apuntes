# Evaluación 1

## MODELO

```text
Tu PC → Frontend (pública) → Backend (privada) → Data (privada)
```

---

## PROGRAMAS (COMANDOS)

Instala por máquina según el rol:

### Frontend

```bash
sudo yum update -y
sudo yum install -y docker git nodejs npm maven
```

### Backend

```bash
sudo yum update -y
sudo yum install -y docker git java-25-amazon-corretto maven
```

### Data

```bash
sudo yum update -y
sudo yum install -y postgresql16 postgresql16-server
```

### Mini verificadores

Ejecuta estos comandos para validar que cada servidor tiene sus herramientas instaladas.

#### Frontend

```bash
docker --version
git --version
node --version
npm --version
mvn --version
```

#### Backend

```bash
docker --version
git --version
java --version
mvn --version
```

#### Data

```bash
psql --version
sudo systemctl status postgresql
```

---

## VARIABLES A REEMPLAZAR

Reemplaza estas variables en todos los comandos con tus valores:

| Variable | Valor | Ejemplo |
| --- | --- | --- |
| `TU_CLAVE.pem` | Nombre de tu archivo clave | `Evaluacion_1.pem` |
| `IP_PUBLICA_FRONTEND` | IP pública del frontend | `3.224.132.173` |
| `IP_PRIVADA_BACKEND` | IP privada del backend | `10.0.138.206` |
| `IP_PRIVADA_DATA` | IP privada del data | `10.0.133.248` |

---

## PASO 1 — Tener tu clave `.pem`

Debes usar **la misma key pair** que usaste al crear las EC2.

### En Windows (Git Bash)

**Si estás en Git Bash:**

```bash
chmod 400 ~/Downloads/TU_CLAVE.pem
```

---

## PASO 2 — Conectarte al FRONTEND (público)

Desde tu PC:

```bash
ssh -i "TU_CLAVE.pem." ec2-user@IP_PUBLICA_FRONTEND
```

>[!note]
>Esto es necesariamente para ver si podemos conectarnos
---

## 🔗 PASO 3 — Copiar tu llave local al servidor Frontend

Ahora estás *dentro* del frontend.

### Opción A (manual: copiar la llave desde tu PC al frontend)

Primero copia la llave al frontend (desde **Git Bash**):

```bash
scp -i TU_CLAVE.pem TU_CLAVE.pem ec2-user@IP_PUBLICA_FRONTEND:/home/ec2-user/
```

Luego estando conectado en frontend (por SSH):

```bash
chmod 400 TU_CLAVE.pem
ssh -i TU_CLAVE.pem ec2-user@IP_PRIVADA_BACKEND
```

> [!important]
> Este PASO 3 corresponde al método manual (copiando la llave `.pem` al frontend).

---

## 🗄️ PASO 4 — Conectarte al DATA

Desde el backend:
Primero copia la llave al frontend (desde **Git Bash**):

```bash
scp -i TU_CLAVE.pem TU_CLAVE.pem ec2-user@IP_PRIVADA_DATA:/home/ec2-user/
```

```bash
ssh -i TU_CLAVE.pem ec2-user@IP_PRIVADA_DATA
```

---

## 🔒 PASO 5 — Security Groups para SSH (MUY IMPORTANTE)

### En `Backend`

Inbound rule:

| Tipo | Puerto | Origen                |
| ---- | ------ | --------------------- |
| SSH  | 22     | Security Group Frontend |

---

### En `Data`

Inbound rule:

| Tipo | Puerto | Origen                                                     |
| ---- | ------ | ---------------------------------------------------------- |
| SSH  | 22     | Security Group Backend |

---

## 🧪 PRUEBAS

Desde frontend:

```bash
ping IP_PRIVADA_BACKEND
```

Desde backend:

```bash
ping IP_PRIVADA_DATA
```

---
