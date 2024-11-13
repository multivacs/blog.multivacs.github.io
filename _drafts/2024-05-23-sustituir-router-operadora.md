---
title: Sustituir el router de operadora por uno Propio + ONT
description: Te explico el proceso para cambiar el router de tu ISP de manera adecuada.
author: mario
date: 2024-05-23 11:33:00 +0000
categories: [Tutoriales, Redes]
tags: [seguridad, privacidad]
pin: false
math: false
mermaid: false
image:
  path: assets/img/posts/2024-05-23-sustituir-router-operadora/sustituir-router.jpg
  alt: Sustituir router.
---

## Índice

1. [Introducción](#introduccion)
2. [Sección 1](#seccion-1)
3. [Sección 2](#seccion-2)
4. [Conclusión](#conclusion)

## Introducción
Recientemente, y tras muchas peleas en llamada para solicitar que me habilitaran la función de modo "bridge" en el router proporcionado por la operadora, sin éxito alguno, decidí tomarme la justicia por mi mano y realizar la sustitución completa del equipo.

Cambiar el router que proporciona tu operadora por uno propio junto con una ONT (Optical Network Terminal) es una decisión que muchos usuarios toman para mejorar el rendimiento, la seguridad y las capacidades de su red doméstica. Este proceso implica algunas consideraciones técnicas previas, y perder la capacidad de gestión remota por parte de la compañía que te ofrezca el servicio; por lo que es algo que sólo recomiendo a aquellos usuarios que como yo, se encuentren en un punto sin salida y deseen deshacerse de las limitaciones de un hardware obsoleto y con pocas prestaciones.

> Si en tu caso, tienes una ONT separada o la posibilidad de poner el router que te instalan en modo puente o **bridge**, y no quieres lidiar con quebraderos de cabeza, ve mejor por esta opción. En ese caso te dejo en [Modo puente](#bridge) el modo de realizarlo.
{: .prompt-tip }


## Conceptos previos
Si no estás familiarizado/a con conceptos como modo bridge, ONT, OLT, credenciales PPoE... quizás todo esto te suene a chino como a mí. Para resumir en pocas palabras, los conceptos importantes con los que te tienes que quedar son:

- **Modo bridge:** esta es una función de la mayoría de routers que vienen con ONT integrada, es decir, la fibra que llega de la calle se conecta directamente al router, y este se encarga de transformar la señal y proporcionarnos acceso a internet. Cuando está habilitada, el router dejaría de actuar como router, y únicamente transformaría la señal. Por lo que luego podríamos colocar nuestro router detrás del de la compañía para proporcionar acceso y gestionar la red.
- **ONT:** como mencionaba anteriormente, la ONT es la que se encarga de recoger la señal óptica de fibra y transformarla en señal eléctrica que un ordenador pueda interpretar. Las hay de varios tipos y marcas, como veremos más adelante.
- **OLT:** una ONT debe de estar siempre en sincronía con una OLT, que básicamente, es un switch ubicado en las instalaciones de la operadora con múltiples puertos para dar servicio de fibra a múltiples abonados. Cuando una operadora te vende un servicio de 1Gb simétrico, realmente, lo que te proporciona es acceso a un puerto de esta OLT que compartes con otros usuarios de la misma zona, ya que como medio de abaratar costes y ser más eficientes, es muy difícil que tú como cliente vayas a consumir ese gigabit/s ideal las 24h del día, lo normal es que se manden paquetes de ida y vuelta que ocupen el canal durante unas milésimas de segundo. Por lo que se comparte la autopista por la que navegamos. Es importante conocer o al menos tener una ligera idea, buscando en foros e informándose, de qué OLT dispone nuestra operadora, ya que como decía al principio, la ONT debe de ser compatible con la OLT para que podamos configurar el acceso.
- **Credenciales PPPoE:** estos son el usuario y contraseña que también deberemos de obtener, de una manera u otra (para esto explico algunos métodos que te pueden servir más adelante), y que sirven para identificarnos contra el ISP.

![GPON](assets/img/posts/2024-05-23-sustituir-router-operadora/arquitectura-pon.jpg){: width="972" height="589" }
_Figura 1: Arquitectura GPON por @Switch-Wifi_