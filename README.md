# TRABAJO-FINAL
TRABAJO FINAL
INSTALCION DE KUBECTL, MINIKUBE Y JUEGO SUPERTUXKART EN KALI LINUX

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




































