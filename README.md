#        FUNDACIÓN UNIVERSITARIA COMPENSAR  -  Facultad de Ingeniería — Telecomunicaciones           

| Año | Institución | Docente |
|--------|--------------|------------|
| 2026 | Fundación Universitaria Compensar | Diego Alejandro Barragán Vargas |

| Integrantes | correo | 
|--------|--------------|

| Integrantes | correo | 
|--------|--------------|
| Alexander Reina | alexanderreina@ucompensar.edu.co |
| Brayan Ivan Ribon Quintero | bribon@ucompensar.edu.co |
| Edwar Roberto Martinez Pinto | ermartinez@ucompensar.edu.co |
| Jeimy Lorena Nino Correa | jlorenanino@ucompensar.edu.co |
| Lina Marcela Contreras Sanabria | lmarcelacontreras@ucompensar.edu.co |

## ¿De qué trata este proyecto?

El proyecto simula una infraestructura de red empresarial real dividida en dos ramas tecnológicas, administradas desde un nodo central con herramientas de monitoreo y seguridad.

La idea nació de un escenario real: una red mal configurada puede tumbar simultáneamente una cirugía remota, una final de videojuegos y una reunión corporativa. Este proyecto demuestra cómo diseñar redes que **no colapsan**.

---

## Arquitectura General

```
                    ┌─────────────────┐
                    │  ADMINISTRADOR  │
                    │  Debian Linux   │
                    │  192.168.51.10  │
                    │  Grafana+Wiresh │
                    └────────┬────────┘
                             │ Gi0/0
                    ┌────────▼────────┐
                    │  ROUTER CISCO   │
                    │     1941        │
                    │  ACL + QoS      │
                    │  DHCP Server    │
                    └────────┬────────┘
                             │ Gi0/1 (Trunk)
                    ┌────────▼────────┐
                    │ SWITCH CATALYST │
                    │  VLAN 20 | 30   │
                    └────┬───────┬────┘
                         │       │
               ┌─────────▼─┐ ┌───▼──────────┐
               │   DOCKER  │ │  KUBERNETES  │
               │192.168.50 │ │ 192.168.49   │
               │           │ │              │
               │ 🐳 YOLO   │ │ ☸️ Minikube  │
               │ 🤖 Chatbot│ │ 🎮 STuxKart  │
               └───────────┘ └──────────────┘
```

### Segmentación de red

| VLAN | Red | Dispositivos |
|------|-----|-------------|
| VLAN 10 | 192.168.51.0/24 | Administrador — Debian + Grafana + Wireshark |
| VLAN 20 | 192.168.50.0/24 | Docker — YOLO + Chatbot |
| VLAN 30 | 192.168.49.0/24 | Kubernetes — SuperTuxKart + Agones |

---

## Rama 1 — YOLO + Chatbot: Detección Inteligente de Logos e Integración de Microservicios en Docker

### ¿Qué hace?

Se desplegaron dos contenedores que trabajan juntos para identificar herramientas tecnológicas y explicarlas en tiempo real.


## Rama 2 — SuperTuxKart en Kubernetes con Agones

### ¿Qué hace?

Se desplegó un servidor dedicado del juego **SuperTuxKart** (clon open-source de Mario Kart) orquestado con **Minikube + Agones** en Kali Linux.

**¿Por qué SuperTuxKart?**
El tráfico UDP que genera el juego compite contra el tráfico de video de YOLO en la red, lo que permite demostrar y medir el funcionamiento de las políticas **QoS** configuradas en el router.


---

## INSTALACIÓN Y CONFIGURACIÓN DEL CHATBOT INTELIGENTE
### Inicialización del Entorno y Control de Contingencia (Fallback)
Al arrancar la aplicación, el script gestiona las librerías esenciales (Flask para el servidor web y requests para las transmisiones HTTP). Un punto clave en el diseño del código es la resiliencia del sistema:

Modo API Externa: El chatbot intenta capturar de forma segura la API Key de Anthropic desde las variables de entorno para conectarse con el modelo de lenguaje natural Claude.

Modo Local (Respuesta Fallback): Si el sistema se despliega en un entorno offline o sin credenciales, se programo una función de contingencia basada en un diccionario de mapeo tecnológico en Python. Esta analiza mediante procesamiento de texto básico las palabras clave del usuario (como Docker, Kubernetes o nmap) y retorna descripciones técnicas precisas de inmediato, garantizando que el chatbot nunca deje de responder.

<img width="702" height="401" alt="image" src="https://github.com/user-attachments/assets/7d2fe3c8-1cb7-4716-b472-75f47edcaff5" />

### Base de Conocimientos Específica (System Prompt)
Para asegurar que el modelo se comporte estrictamente como el asistente oficial de nuestro proyecto, se inyecto un System Prompt estructurado. En esta base de conocimientos se definio al chatbot el contexto exacto de nuestra arquitectura de tres contenedores (YOLO, Parrot OS y el propio Chatbot) y se le proporciono la documentación conceptual de cada herramienta. Con esto se logro acotar las respuestas de la IA para que sean concisas, didácticas y enfocadas 100% en los requerimientos académicos de la entrega.

<img width="1365" height="639" alt="image" src="https://github.com/user-attachments/assets/a82c99cd-b8b0-4618-9bb1-2c09580110f0" />

### Arquitectura de Endpoints y Rutas del Servidor
El servidor de Flask expone tres rutas principales orientadas al control del flujo de datos:

Ruta Raíz (/): Renderiza el archivo index.html de la interfaz gráfica, la cual cuenta con un diseño cyber-tech optimizado y hojas de estilo que integran la Web Speech API del navegador para habilitar la lectura por voz.

Ruta de Mensajería (/chat): Procesa las consultas de texto plano enviadas por el usuario, manteniendo un buffer de los últimos 10 mensajes para preservar el hilo conversacional (historial) antes de solicitar la inferencia lingüística.

### Integración Concurrente y Redirección de Puertos (/detectar)
Esta es la sección más crítica del desarrollo, ya que consolida la comunicación interactiva entre microservicios (Chatbot y YOLO). Para evitar colisiones de red en entornos locales (el error Address already in use), se tomo la decisión arquitectónica de aislar los puertos, asignando el puerto 5001 para el Chatbot y el puerto 5000 para el servidor de YOLO.

El flujo de integración síncrona que se programo funciona de la siguiente manera:

El usuario carga la imagen de un logotipo tecnológico desde la interfaz del Chatbot (Puerto 5001).

El endpoint /detectar procesa el archivo y, mediante una petición HTTP POST utilizando la librería requests, actúa como un puente de red enviando los bytes de la imagen a la dirección local de YOLO ([http://127.0.0.1:5000/api/clasificar](http://127.0.0.1:5000/api/clasificar)).

El script de YOLO ejecuta la inferencia con su modelo entrenado y me retorna un objeto estructurado en formato JSON con la etiqueta de la herramienta identificada y su porcentaje de confianza.

El código recibe este veredicto, genera de forma automatizada una consulta aclaratoria sobre esa tecnología y le solicita al motor de IA que formule una explicación educativa en tiempo real para desplegarla al usuario en la web junto con el porcentaje de acierto.

### Arranque y Despliegue del Servicio
Finalmente, el bloque principal del programa inicializa el demonio de Flask exponiendo la aplicación en la dirección 0.0.0.0 para permitir conexiones desde cualquier interfaz de red del host, fijando de manera estricta el puerto de escucha en el 5001 y activando el modo debug para agilizar el monitoreo de errores en tiempo de desarrollo.

<img width="1365" height="720" alt="image" src="https://github.com/user-attachments/assets/d2c2aff8-bffd-448f-ac37-356eabff9c70" />
<img width="1365" height="680" alt="image" src="https://github.com/user-attachments/assets/280e6ae0-96b5-4907-b7f9-da3b2027b0bd" />

## INSTALCION DE KUBECTL, MINIKUBE Y JUEGO SUPERTUXKART EN KALI LINUX

Se realiza la actulización y descarga de paquetes nuevo para el kali linux

<img width="1362" height="263" alt="Captura desde 2026-05-25 17-26-23" src="https://github.com/user-attachments/assets/38200dfa-f8ba-4e4c-a47d-9b982fce1ae4" />

Luego se instala las dependencias para la instancia de gpg

<img width="866" height="366" alt="Captura desde 2026-05-25 17-33-43" src="https://github.com/user-attachments/assets/c2421a14-9d47-48d6-a332-e4264d3d3421" />

se descarga luego k8s para vincularlo con el kubectl y se valida la descarga 

<img width="960" height="157" alt="Captura desde 2026-05-25 17-34-53" src="https://github.com/user-attachments/assets/1845dbe4-a4b0-428c-85ad-cd921eac8cfc" />

asi mismo se instala minikube (el contenedor donde se instalara el juego supertuxkart)

<img width="730" height="141" alt="Captura desde 2026-05-25 17-39-18" src="https://github.com/user-attachments/assets/6eedec36-93db-4220-a35a-e365645f98dd" />

Despues se procede a instalar Docker.io, anteriormente ya se habia instalado asi que solo actulizo las nuevas version que se encuentra en linea.

<img width="890" height="454" alt="Captura desde 2026-05-25 17-50-54" src="https://github.com/user-attachments/assets/720020c4-1d62-460a-8e06-0ff7211baa4d" />

Ahora se procedera a correr los drivers en el minikube con la instancia de --force

<img width="920" height="235" alt="Captura desde 2026-05-25 17-51-34" src="https://github.com/user-attachments/assets/e341d883-ad52-458f-9e3b-13f7c99a8931" />

<img width="1044" height="472" alt="Captura desde 2026-05-25 17-52-07" src="https://github.com/user-attachments/assets/8cb8f731-c192-4690-b16a-e858f4e9bc42" />

Se realiza la creación de del cluster-admin-binding


<img width="824" height="133" alt="Captura desde 2026-05-25 17-52-33" src="https://github.com/user-attachments/assets/9146d22a-00a5-42e9-a2f8-20e4b7130fa5" />

Luego se valida el estado de los pods del kuberctl

<img width="868" height="394" alt="Captura desde 2026-05-25 17-54-29" src="https://github.com/user-attachments/assets/e59f3dbb-578a-493d-aeb5-7d74cb1f1d04" />

Se instala luegp hubusercontent donde se dirigira al bash

<img width="826" height="173" alt="Captura desde 2026-05-25 17-55-06" src="https://github.com/user-attachments/assets/c1c5e214-3a2d-414e-90c7-795f991c6f7b" />

Despues se agregara la instancia de agones para tomar la dependencia de snap

<img width="622" height="138" alt="Captura desde 2026-05-25 17-57-33" src="https://github.com/user-attachments/assets/4db26572-4793-4559-98e3-468d284c0a74" />

Luego se crea el namespace para agones

<img width="696" height="161" alt="Captura desde 2026-05-25 17-58-50" src="https://github.com/user-attachments/assets/b1de0152-75e7-427c-b310-72fa6fd7c4aa" />

se determina el pods de agones

<img width="638" height="235" alt="Captura desde 2026-05-25 17-59-23" src="https://github.com/user-attachments/assets/f9385775-7e22-4f74-a461-1828ebb7e5a7" />

Asi mismo se determina que direccion ip esta tomando minikube


<img width="505" height="74" alt="Captura desde 2026-05-25 17-59-55" src="https://github.com/user-attachments/assets/bdf643da-c959-4a1f-8c4f-53e25e1cf347" />

Se realiza una validacion de para supertuxkart-server.yaml

<img width="661" height="503" alt="Captura desde 2026-05-25 18-00-44" src="https://github.com/user-attachments/assets/183b89a4-e6e1-449d-8665-3ab3d133e498" />

se redirige a la ruta de kubectl el supertuxkart-server.yaml

<img width="461" height="82" alt="Captura desde 2026-05-25 18-01-13" src="https://github.com/user-attachments/assets/0c3df66e-6248-4156-9774-6f4f7277c420" />

se determina la direccion ip del gameservers

<img width="547" height="79" alt="Captura desde 2026-05-25 18-01-38" src="https://github.com/user-attachments/assets/6f6f1dc4-f99b-43b4-a05e-1d85c547a83a" />

se valida tambien la descripción del gameserver para el supertuxkart

<img width="594" height="653" alt="Captura desde 2026-05-25 18-02-52" src="https://github.com/user-attachments/assets/a93f9acd-a0ef-462f-a828-8ffabd023b3b" />
<img width="707" height="665" alt="Captura desde 2026-05-25 18-03-07" src="https://github.com/user-attachments/assets/c0ddfd3a-b60f-48b7-afdd-05b5276de949" />

Despues se realiza la instalación de supertuxkart

<img width="806" height="395" alt="Captura desde 2026-05-25 18-04-52" src="https://github.com/user-attachments/assets/53776861-43e0-4592-a7b5-d3970eda40e8" />

para despues con el comando: supertuxkart automaticamente se abrir el juego.

NOTA: antes se realizar la instalación de supertuxkart se debera registrarse en la pagina oficial de supertuxkart link de registro: https://online.supertuxkart.net/login.php


Y este es el resultado de la instalación:

<img width="1360" height="768" alt="Captura desde 2026-05-25 20-57-41" src="https://github.com/user-attachments/assets/d9739216-7a44-4830-becf-64641128a61c" />

y desde la consola de kali linux se puede ver en tiempo real la ejecucion del juego


<img width="1360" height="768" alt="Captura desde 2026-05-25 21-14-13" src="https://github.com/user-attachments/assets/5430c5df-1554-41bc-b3c0-9bce21107e18" />
<img width="1360" height="768" alt="Captura desde 2026-05-25 21-14-20" src="https://github.com/user-attachments/assets/605fed08-520a-4dc4-aa03-a9b59903055e" />

se selecciona una partida y el personaje

<img width="1011" height="674" alt="Captura desde 2026-05-25 21-19-00" src="https://github.com/user-attachments/assets/54610b00-9cca-4251-bba3-10b51dbcf80b" />

los modos del juego

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-30-22" src="https://github.com/user-attachments/assets/5a22193a-e81a-46b8-94b8-b3751d9b644c" />

se realizara una red local para jugar contra "maquina" (boot)

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-30-30" src="https://github.com/user-attachments/assets/a32f342e-a4c5-44d8-a44d-c208acec89ab" />

se crea un servidor

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-30-38" src="https://github.com/user-attachments/assets/5e59f096-f0ab-44f1-9ad1-cdada4689ea6" />

las opciones de juego (se toma cuantos kart manejara el ordenador "maquina")

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-30-53" src="https://github.com/user-attachments/assets/cd5bb721-8ce3-4987-9c13-0501474f6e0b" />

visualizacion de los jugadores

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-31-00" src="https://github.com/user-attachments/assets/9bce9132-5373-43b3-b288-749c60e2dd93" />

selección del personaje

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-31-07" src="https://github.com/user-attachments/assets/a7b32dd8-7b98-4bb7-a3ce-3b87b736c777" />

tipo de circuito

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-31-15" src="https://github.com/user-attachments/assets/bbf78325-62ac-481b-a62d-b865b450c8a8" />

y este seria el resultado final donde se compite con otro personajes del juego

<img width="1022" height="742" alt="Captura desde 2026-05-25 21-31-37" src="https://github.com/user-attachments/assets/e729ef5f-bed3-492d-bfb1-fbc064911158" />
<img width="1022" height="742" alt="Captura desde 2026-05-25 21-31-53" src="https://github.com/user-attachments/assets/a1641a5d-15ee-452d-b7f1-16a49fe87530" />
<img width="1022" height="742" alt="Captura desde 2026-05-25 21-31-46" src="https://github.com/user-attachments/assets/6f7ddb2b-ed35-4833-ad9b-6a69c7e2e683" />

Se analiza el comportamiento del juego con wireshark

<img width="1366" height="726" alt="Captura desde 2026-05-27 23-13-17" src="https://github.com/user-attachments/assets/31afded1-6fab-4cd8-8acc-cc48aa794cf9" />

# Configuracion de equipos fisicos, Router y Switch

## SWITCH CATALYST - CONFIGURACIÓN DE VLANs

! --- Crear las 3 VLANs ---


<img width="498" height="361" alt="image" src="https://github.com/user-attachments/assets/4661a4e2-6612-4831-9f4a-a9bdf2167ab8" />


<img width="1025" height="837" alt="image" src="https://github.com/user-attachments/assets/d94acbbd-b310-45c2-804a-b5b88a1332d5" />

## ROUTER CISCO 1941 - INTERFAZ ADMINISTRADOR


<img width="813" height="341" alt="image" src="https://github.com/user-attachments/assets/d7305dbc-f0d2-41cb-afa4-8f40ee036de2" />

## SUBINTERFACES PARA VLAN DOCKER Y KUBERNETES


<img width="757" height="139" alt="image" src="https://github.com/user-attachments/assets/a9aa393e-cc0d-41f2-bcc4-f77d4bab9415" />


<img width="877" height="187" alt="image" src="https://github.com/user-attachments/assets/df352699-1b55-42e2-8a45-7d82b10f527f" />

## Verificacion de la creacion de las Vlan de Docker y Kubernetes


<img width="1107" height="234" alt="image" src="https://github.com/user-attachments/assets/735e5eea-4ed5-464a-9ac8-54faf6e8c9fc" />

-Subinterfaz VLAN 20 - Docker
-Subinterfaz VLAN 30 - Kubernetes

## Pool DHCP para Docker


<img width="1125" height="614" alt="image" src="https://github.com/user-attachments/assets/ea64e191-8916-4aa4-9b16-e07d262ab501" />

# YOLO + Chatbot: Detección Inteligente de Logos e Integración de Microservicios en Docker
Esta sección del proyecto implementa dos servicios inteligentes que corren dentro de contenedores Docker y se comunican entre sí de forma automática:

1. **YOLO** — Un clasificador de logos de herramientas tecnológicas usando inteligencia artificial
2. **Chatbot** — Un asistente que explica cada herramienta detectada, con soporte de voz e imágenes

Todo está diseñado para que funcione en cualquier computador con Docker instalado, sin necesidad de configuraciones complicadas.

---

## ¿Cómo funciona YOLO en este proyecto?

YOLO (You Only Look Once) es un modelo de inteligencia artificial que analiza imágenes y las clasifica en fracciones de segundo. En este proyecto lo entrenamos desde cero para que reconozca logos de herramientas de infraestructura tecnológica.

### ¿Qué herramientas detecta?

| Logo | Herramienta | ¿Para qué se usa? |
|------|------------|-------------------|
| 🐳 | Docker | Crear y gestionar contenedores |
| ☸️ | Kubernetes | Orquestar contenedores a escala |
| 🤖 | Jenkins | Automatizar despliegues de software |
| 📦 | Ansible | Configurar servidores automáticamente |
| 🏗️ | Terraform | Crear infraestructura como código |
| 🦭 | Podman | Alternativa a Docker sin permisos root |
| 📊 | Grafana | Visualizar métricas y dashboards |

### ¿Cómo lo entrenamos?

Como no teníamos miles de imágenes disponibles, usamos una técnica llamada **Data Augmentation**: tomamos pocas imágenes base de cada logo y generamos variaciones automáticas aplicando rotaciones, cambios de brillo y contraste. Esto le enseñó al modelo a reconocer los logos aunque estén en diferentes posiciones o condiciones de luz.

El entrenamiento duró **30 épocas** y el modelo alcanzó un **100% de precisión** en el conjunto de validación.

### ¿Cómo se expone el servicio?

El modelo corre dentro de un contenedor Docker con un servidor web Flask. Expone dos rutas:

- `GET /` → Interfaz web para subir imágenes manualmente
- `POST /api/clasificar` → API que recibe una imagen y retorna el nombre de la herramienta detectada en formato JSON

---

## 🤖 ¿Cómo funciona el Chatbot?

El chatbot es el asistente oficial del proyecto. Su diseño tiene tres características principales:

### 1. Modo con API / Modo sin API (Fallback)
El sistema está preparado para dos escenarios:

- **Con API Key de Anthropic**: usa el modelo Claude para generar respuestas elaboradas y naturales
- **Sin API Key (offline)**: activa automáticamente una base de conocimiento local que responde sobre todas las herramientas del proyecto sin necesidad de internet

Esto garantiza que el chatbot **nunca deje de funcionar**, independientemente del entorno donde se despliegue.

### 2. Base de conocimiento del proyecto (System Prompt)
Se programó un prompt de sistema que le indica al modelo exactamente quién es y qué sabe: la arquitectura del proyecto, los tres contenedores, y las herramientas tecnológicas involucradas. Así las respuestas siempre son relevantes y educativas para el contexto académico.

### Tres formas de interactuar

| Modo | Descripción |
|------|-------------|
| ✍️ Texto | Escribe tu pregunta y recibe respuesta inmediata |
| 🎤 Voz | Habla por el micrófono y el chatbot responde en voz alta usando la Web Speech API del navegador |
| 📷 Logo | Sube una imagen de un logo → el chatbot llama a YOLO, obtiene la clasificación y genera una explicación automática |

<img width="1917" height="592" alt="image" src="https://github.com/user-attachments/assets/9080e827-289a-4197-a341-ce3b90d29f4a" />

<img width="1902" height="993" alt="image" src="https://github.com/user-attachments/assets/c58a06eb-ea41-4143-9ec6-2c7870f439e6" />

---

## Comunicación entre contenedores

La parte más importante de la implementación es cómo YOLO y el Chatbot se comunican. Ambos corren en la misma red interna de Docker llamada `proyecto-net`, lo que les permite llamarse por nombre de servicio.

```
[Usuario en el navegador]
        │
        ▼
[Chatbot - Puerto 5001]
        │ Sube imagen de logo
        ▼
[YOLO - Puerto 5000] ──► Clasifica el logo ──► Retorna JSON
        │                {"herramienta": "docker", "confianza": 100}
        ▼
[Chatbot] ──► Genera explicación ──► Muestra resultado al usuario
```

Para que funcionen juntos se usa `docker-compose`, que levanta ambos contenedores en la misma red y permite que se comuniquen usando sus nombres (`yolo` y `chatbot`) como si fueran dominios internos.

<img width="1902" height="218" alt="image" src="https://github.com/user-attachments/assets/f2aed1a1-e42e-4296-8d3d-180a93cd01c0" />

<img width="1918" height="401" alt="image" src="https://github.com/user-attachments/assets/a5aa9bf3-1a60-4af3-b030-6b41df30e15f" />


---

## Requisitos para correrlo

- Docker Desktop instalado y corriendo
- Windows 10/11 o Linux
- ~3GB de espacio libre
- Conexión a internet solo para el primer build

---

## Cómo iniciar el proyecto

**Levantar todo:**
```bash
docker compose up -d
```

**Abrir en el navegador:**
- Clasificador YOLO → http://localhost:5000
- Chatbot → http://localhost:5001

**Apagar todo:**
```bash
docker compose down
```

---

## 📁 Estructura de archivos

```
proyecto_final/
├── yolo/
│   ├── app.py              # Servidor Flask + inferencia YOLO
│   ├── Dockerfile          # Python 3.10 + PyTorch CPU + Ultralytics
│   └── models/
│       └── best.pt         # Modelo entrenado (7 clases, 100% accuracy)
│
├── chatbot/
│   ├── app.py              # Servidor Flask + lógica del chat + fallback
│   ├── Dockerfile          # Python 3.10 + Flask + Requests
│   └── templates/
│       └── index.html      # Interfaz web (texto + voz + imagen)
│
└── docker-compose.yml      # Orquesta los dos servicios en red compartida
```

<img width="1007" height="325" alt="image" src="https://github.com/user-attachments/assets/a9fc046a-5539-4107-bc94-632385ae8543" />

<img width="1052" height="338" alt="image" src="https://github.com/user-attachments/assets/385ac56c-e88b-4971-8d22-b4fb65336a5a" />


---

## Tecnologías utilizadas

| Tecnología | Uso |
|-----------|-----|
| Docker + Docker Compose | Contenedores y red interna |
| Python 3.10 | Lenguaje de backend |
| YOLOv8 (Ultralytics) | Modelo de clasificación de imágenes |
| PyTorch CPU | Motor de inferencia del modelo |
| Flask | Servidor web de ambos contenedores |
| Web Speech API | Voz en el chatbot (nativa del navegador) |
| Anthropic Claude (opcional) | Motor de lenguaje natural del chatbot |


#   CRACION DE IMÁGENES EN ROBOFLOW PARA EL LOGO DE DOCKER  
 
#  https://roboflow.com/

1.	Usamos la opción en la página web de aumento de datos usando modificaciones de una cantidad pequeñas de imágenes.

2.	Generamos una nueva versión y la vamos guardando.


3.	Preprocesamiento y aumento de datos, cada argumentación crea nuevas variantes de tus imágenes.

4.	Aumentando la cantidad de imágenes de 10 en 10 hasta completar las 100 imágenes solicitadas.


5.	Generar dataset, Roboflow empezará a crear automáticamente las imágenes nuevas.

6.	Entrenar modelo para descargar el dataset d eimagenes.


7.	Exportadas en formato para YOLOv8.

   #  ADMINISTRADOR
      Debian Linux
      IP: 192.168.51.10
      Grafana + Wireshark                     
      Puerto: Gi0/0

<img width="1163" height="654" alt="image" src="https://github.com/user-attachments/assets/e1a70882-4bcc-472c-9c6b-126f8d49e991" />

<img width="1135" height="639" alt="image" src="https://github.com/user-attachments/assets/3dc76f2d-ab68-4ad5-9363-34ebf2815185" />

<img width="1115" height="626" alt="image" src="https://github.com/user-attachments/assets/1d9672b7-4a96-451b-9201-70fbbaed5437" />

<img width="1124" height="632" alt="image" src="https://github.com/user-attachments/assets/081733f2-85d7-4768-aae6-bcf9f9aacf65" />


# CONFIGURACIÓN E INSTALACIÓN DE DEBÍAN 13.5

#   Software free VirtualBox para instalación de Debian 13.5

#   Configuración Inicial:


<img width="1080" height="572" alt="image" src="https://github.com/user-attachments/assets/00ace63b-922a-4dbd-852e-003fe4b396e2" />


<img width="1087" height="611" alt="image" src="https://github.com/user-attachments/assets/11ba0a2f-17ac-491d-98ff-12f6ad9a64a7" />


<img width="1130" height="593" alt="image" src="https://github.com/user-attachments/assets/087cf2d7-f25c-45c7-acc2-1270ddfafe89" />


#   CONFIGURACIÓN E INSTALACIÓN DE WIRESHARK EN DEBIAN


<img width="1087" height="573" alt="image" src="https://github.com/user-attachments/assets/86ea7240-b858-4968-a1c2-c7d77b4166e3" />


<img width="997" height="796" alt="image" src="https://github.com/user-attachments/assets/fd6bf137-9549-486d-98fc-c6939cfed40f" />


<img width="1075" height="458" alt="image" src="https://github.com/user-attachments/assets/f498e519-2c8c-42a6-84aa-e90d92669ff2" />


<img width="1089" height="572" alt="image" src="https://github.com/user-attachments/assets/99d94f6a-d63b-40c9-b1bd-4933e94f2cc6" />


<img width="1129" height="598" alt="image" src="https://github.com/user-attachments/assets/2885c873-616f-46dc-ac4b-f80ae15566e8" />


#   CONFIGURACIÓN E INSTALACIÓN DE GRAFANA DASHBOARD EN DEBIAN


<img width="1097" height="565" alt="image" src="https://github.com/user-attachments/assets/aac8487d-26e6-464a-85d5-9cf2f4800cde" />


<img width="1117" height="591" alt="image" src="https://github.com/user-attachments/assets/afb6acff-6306-404c-8543-e4f084151581" />


<img width="1098" height="652" alt="image" src="https://github.com/user-attachments/assets/547648c6-4437-42dc-849e-6684ef5a28ae" />


<img width="1143" height="607" alt="image" src="https://github.com/user-attachments/assets/a76f01ae-bac6-4a16-85de-5daff938625a" />


<img width="1119" height="607" alt="image" src="https://github.com/user-attachments/assets/2a7fdfbe-37a7-42c0-9731-c6ecd384e272" />


<img width="1097" height="589" alt="image" src="https://github.com/user-attachments/assets/fc86321c-5f95-470f-a210-10390793a2a1" />


#   CONFIGURACIÓN DE IP ESTÁTICA EN DEBIAN 13.
#   Ejecutamos la consola como administradores en debian en virtualbox:
 
#   En VirtualBox configura el adaptador de red de la VM Debian así:
#   Configuración de comandos en Debian IP estática:

    auto enp0s3
    iface enp0s3 inet static    
    address 192.168.51.10    
    netmask 255.255.255.0   
    gateway 192.168.51.1   
    dns-nameservers 8.8.8.8

    sudo systemctl restart networking

    ip a
    ping 192.168.51.1

<img width="1101" height="535" alt="image" src="https://github.com/user-attachments/assets/3fd1bc24-4316-4a74-a71e-b7361595046a" />





