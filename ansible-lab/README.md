# Laboratorio de Ansible con Docker

## Objetivo

Administrar dos contenedores Ubuntu 24.04 con Ansible: consultar su nombre y sistema operativo, crear archivos y directorios, y mostrar un mensaje condicionado a que el sistema sea Ubuntu.

## Requisitos

- Docker Engine y Docker Compose.
- Ansible instalado en el equipo anfitrión.
- El plugin de conexión Docker de la colección `community.docker`.

Instala la colección si aún no está disponible:

```bash
ansible-galaxy collection install community.docker
```

## Iniciar los contenedores

Desde esta carpeta (`ansible-lab`):

```bash
docker compose up -d
docker ps
```

Instala Python 3 en ambos contenedores, necesario para que Ansible ejecute módulos:

```bash
docker exec server1 bash -c "apt update && apt install -y python3"
docker exec server2 bash -c "apt update && apt install -y python3"
```

## Comprobar la conexión

```bash
ansible docker -i inventory.ini -m ping
```

## Ejecutar el playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

El playbook muestra los datos de cada servidor, crea `/tmp/ansible-demo/info.txt` y los directorios `logs`, `backup` y `config`. El mensaje de Ubuntu aparece únicamente cuando el sistema operativo detectado es Ubuntu.

## Captura de la ejecución exitosa

Guarda aquí la captura de la ejecución exitosa con el nombre `captura-playbook.png`:

![Captura de la ejecución exitosa del playbook](captura-playbook.png)
