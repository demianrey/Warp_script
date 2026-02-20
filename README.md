# 【WGCF】Conectar CF WARP para agregar red IPv4/IPv6 a servidores

* * *

# Tabla de Contenidos

- [Información de Actualizaciones](#información-de-actualizaciones)
- [Características del Script](#características-del-script)
- [Beneficios de WARP](#beneficios-de-warp)
- [Uso del Script WARP](#uso-del-script-warp)
- [Uso del Script WARP-GO](#uso-del-script-warp-go)
- [API de Cloudflare](#api-de-cloudflare)
- [Cómo obtener una IP WARP desbloqueada para Netflix](#cómo-obtener-una-ip-warp-desbloqueada-para-netflix)
- [Plantilla de enrutamiento WARP socks5 o interface y desbloqueo de chatGPT](#plantilla-de-enrutamiento-warp-socks5-o-interface-y-desbloqueo-de-chatgpt)
- [Obtención de WARP+ License e ID](#obtención-de-warp-license-e-id)
- [Cómo obtener y usar WARP Teams en Linux](#cómo-obtener-y-usar-warp-teams-en-linux)
- [Principio de WARP](#principio-de-warp)
- [Agradecimientos a los Contribuidores de WARP y Estado del Servicio Global de CloudFlare WARP](#agradecimientos-a-los-contribuidores-de-warp-y-estado-del-servicio-global-de-cloudflare-warp)

* * *

## Información de Actualizaciones

2026.01.02 mehu.sh v3.2.0 / warp-go.sh v1.3.0 1. Cuentas: Se eliminaron los tipos de cuenta WARP+ y Teams obsoletos del proceso de instalación y actualización (warp a) siguiendo los ajustes de Cloudflare; 2. Corrección de Bug: Se resolvió la interrupción de red corrigiendo el manejo de reglas de enrutamiento durante la eliminación del Linux Client en modo proxy; 3. Rendimiento: Se implementó una IP API propia para mejorar significativamente la velocidad de obtención de información de IP; 4. Limpieza: Se eliminaron mensajes de script obsoletos y mensajes de UI redundantes; 5. Lógica de renovación de IP: Se ajustó la preferencia predeterminada de desbloqueo de Netflix de IPv4 a IPv6

2025.09.10 menu.sh v3.1.8 Mejorada la compatibilidad del script con los sistemas Arch Linux y EndeavourOS.

2025.08.24 menu.sh v3.1.7 1. Soporte añadido para instalar Warp en Ubuntu 24.04 y versiones posteriores. Gracias a la solución del miembro de la comunidad [Michaol]; 2. Soporte añadido para la instalación de Client en Debian 13. Gracias al feedback del usuario [ainp]

<details>
    <summary>Actualizaciones históricas (clic para expandir o contraer)</summary>
<br>

>2025.08.11 menu.sh v3.1.6 / warp-go.sh v1.2.4 Se eliminó la función de mejor endpoint para adaptarse a los ajustes oficiales
>
>2025.03.24 menu.sh v3.1.5 1. Se corrigió el modo Warp (interfaz de red) del Client para que funcione tras reinicio; 2. Se corrigió la expresión regular de validación de Team IPv6
>
>2024.12.24 menu.sh v3.1.4 / warp-go.sh v1.2.3 Soporte para Docker escuchando externamente en 0.0.0.0/0 sin requerir modo de red host. Gracias a @Anthony_Tel
>
>2024.9.24 menu.sh v3.1.3 El Linux Client añade la opción del protocolo MASQUE, disponible tanto en modo Proxy (menú 5) como en modo WarpProxy (menú 14)
>
>2024.9.14 menu.sh v3.1.2 / warp-go.sh v1.2.2 1. Se eliminó la función de generación de licencias ya que clonar licencias Warp+ está prohibido oficialmente; 2. Se eliminó la dependencia innecesaria de python3
>
>2024.7.25 menu.sh v3.1.1 / warp-go.sh v1.2.1 1. Soporte para usar la API WARP propia en https://warp.cloudflare.now.cc/?run=pluskey para generar una licencia WARP+ de 1920 PB; 2. El Client no tiene soporte suficiente para WARP+, solo IPv4; 3. Instalador optimizado para reducir el tiempo de ejecución
>
>2024.7.18 menu.sh v3.1.0 / warp-go.sh v1.2.0 1. Usar la API warp propia: https://warp.cloudflare.now.cc/ para actualizar a cuenta Teams; 2. La configuración del Client requiere ajustes en el panel de Cloudflare, por lo que no se actualizó automáticamente a cuenta Teams
>
>2024.7.8 menu.sh v3.0.10 / warp-go.sh v1.1.9 1. Publicación de la API warp, permite registrar cuentas, unirse a Zero Trust, consultar información de cuenta y más; 2. Scripts actualizados con la API warp
>
>2024.6.30 menu.sh v3.0.9 1. Procesamiento paralelo de MTU óptimo, endpoint óptimo, descarga de wireguard-go e instalación de dependencias mediante multithreading, reduciendo el tiempo de ejecución a más de la mitad; 2. Proxy inverso con Cloudflare worker para mejor soporte dual-stack y mayor velocidad; 3. Prioridad DNS: Cloudflare 1.1.1.1 > Google 8.8.8.8
>
>2024.6.28 menu.sh v3.0.8 El WARP Linux Client oficial soporta sistemas arm64, disponible en modo socks5 proxy y modo Warp interface
>
>2024.6.2 menu.sh v3.0.7 Soporte para CentOS 9 / Alma Linux 9 / Rocky Linux 9
>
>2024.5.5 menu.sh v3.0.6 / warp-go.sh v1.1.8 Soporte para Alpine edge
>
>2024.5.1 menu.sh v3.0.5 Manejo de cambios en repositorio apt de Debian 10 para wireguard-tools
>
>2024.4.14 menu.sh v3.0.4 1. Alpine verifica y actualiza la versión de wget; 2. Mensaje informativo cuando falla la conexión WARP
>
>2024.3.21 menu.sh v3.0.3 / warp-go.sh 1.1.7 1. Actualización de comandos según warp-cli oficial; 2. Se eliminó el CDN de Github
>
>2024.2.7 menu.sh v3.0.2 Verificar si el módulo del kernel WireGuard está cargado, intentar cargarlo si no y verificar nuevamente
>
>2023.12.19 menu.sh v3.0.1 / warp-go.sh 1.1.6 Verificación de UDP permitido; si todos los endpoints de WARP son inalcanzables, el script se detiene
>
>2023.8.22 menu.sh v3.0.0 / warp-go.sh 1.1.5 Añadir CDN de Github
>
>2023.8.15 menu.sh v3.0.0 1. Modo de trabajo no-global; se puede cambiar con [warp g], requiere reinstalación del script; 2. Soporte para regiones sancionadas por Cloudflare (ej: Rusia) con cuenta compartida; 3. IPv6 only usa nat64 preconfigurado y restaura el nameserver original al desinstalar
>
>2023.7.21 menu.sh v3.0.0 beta2 1. Posibilidad de cambiar entre kernel wireguard y wireguard-go-reserved con [warp k]; 2. Soporte para Fedora; 3. Corrección de error de switch en client versión 2023.7.40-1
>
>2023.6.30 menu.sh v3.0.0 beta ACTUALIZACIÓN IMPORTANTE: 1. Uso de la API oficial de Cloudflare warp en reemplazo de wgcf; 2. Uso de wireguard-go with reserved en lugar del kernel; 3. Por los grandes cambios, se pide a los usuarios reinstalar

</details>

## Características del Script

* Soporte para cuenta WARP+, con scripts de terceros para actualizar el tráfico WARP+ y el kernel BBR
* Menú amigable para usuarios normales, los usuarios avanzados pueden configurar rápidamente usando opciones de sufijo
* Detección inteligente del sistema operativo del VPS: Ubuntu 16.04, 18.04, 20.04; Debian 9, 10, 11, CentOS 7, 8; Alpine y Arch Linux. Se recomienda elegir un sistema LTS
  Detección inteligente del tipo de arquitectura de hardware: AMD, ARM y s390x
* Combinando la versión de Linux y el método de virtualización, optimiza automáticamente tres soluciones WireGuard.
  Rendimiento de red: WireGuard integrado en el kernel > Instalar módulo del kernel > BoringTun > wireguard-go
* Detección inteligente de la versión más reciente del repositorio github del autor de WGCF (Latest release)
* Análisis inteligente de IP interna y pública para generar el archivo de configuración WGCF
* Muestra resultados, indica si se usa IP WARP y la ubicación de la IP

## Beneficios de WARP

* Soporte para chatGPT, desbloqueo de Netflix y otros medios de streaming
* Evitar el captcha de Google o usar Google Académico
* Permite llamar a interfaces IPv4, para que proyectos como Qinglong y V2P funcionen normalmente
* Al poder transmitir datos en ambas direcciones, puede usarse como puente y sonda del VPS de otro, reemplazando HE tunnelbroker
* Permite que los nodos construidos en VPS con solo IPv6 soporten Telegram
* Los nodos construidos con IPv6 pueden usarse en PassWall y ShadowSocksR Plus+ que solo soportan IPv4

<img src="https://user-images.githubusercontent.com/62703343/144635014-4c027645-0e09-4b84-8b78-88b41f950627.png" width="80%" />

## Uso del Script WARP

Primera ejecución
```
wget -N https://raw.githubusercontent.com/demianrey/Warp_script/refs/heads/mod/menu.sh && bash menu.sh [opción] [licencia/url/token]
```
Ejecuciones posteriores
```
warp [opción] [licencia]
```
  | [opción] Variable1 Variable2 | Descripción de la acción |
  | ----------------- | --------------- |
  | h | Ayuda |
  | 4 | Estado original -> WARP IPv4 |
  | 4 licencia nombre | Añadir WARP+ License y nombre de dispositivo, ej: ```bash menu.sh 4 N5670ljg-sS9jD334-6o6g4M9F Goodluck``` |
  | 6 | Estado original -> WARP IPv6 |
  | d | Estado original -> WARP doble pila |
  | o | Switch WARP, el script juzga el estado actual y activa/desactiva automáticamente |
  | u | Desinstalar WARP |
  | n | Para renovar la red WARP cuando hay desconexión (bug de WARP) |
  | b | Actualizar kernel, habilitar BBR y DD |
  | p | Renovar tráfico Warp+ |
  | c | Instalar WARP Linux Client, habilitar modo proxy Socks5 |
  | l | Instalar WARP Linux Client, habilitar modo WARP |
  | c licencia | Añadir WARP+ License a lo anterior, ej: ```bash menu.sh c N5670ljg-sS9jD334-6o6g4M9F``` |
  | r | Switch del WARP Linux Client |
  | v | Sincronizar el script a la última versión |
  | i | Cambiar IP de WARP |
  | e | Instalar solución de enrutamiento iptables + dnsmasq + ipset |
  | w | Instalar solución WireProxy |
  | y | Switch de WireProxy |
  | k | Cambiar entre kernel wireguard / wireguard-go-reserved |
  | g | Cambiar WARP global / no-global o instalar en modo no-global por primera vez |
  | s | s 4/6/d, cambiar prioridad warp IPv4 / IPv6 / default del VPS |
  | Otro o vacío | Interfaz de menú |

Ejemplo: Para añadir doble pila Warp a un Oracle IPv4 por primera vez
```
wget -N https://raw.githubusercontent.com/demianrey/Warp_script/refs/heads/mod/menu.sh && bash menu.sh d
```
Renovar IP de Netflix de Japón
```
warp i jp
```


## Uso del Script WARP-GO

Primera ejecución
```
wget -N https://raw.githubusercontent.com/demianrey/Warp_script/main/warp-go.sh && bash warp-go.sh [opción] [licencia]
```
Ejecuciones posteriores
```bash
warp-go [opción] [licencia]
```
  | [opción] Variable1 Variable2 | Descripción de la acción |
  | ----------------- | --------------- |
  | h | Ayuda |
  | 4 | Estado original -> WARP IPv4 |
  | 4 licencia nombre | Añadir WARP+ License y nombre de dispositivo, ej: ```bash wire-go 4 N5670ljg-sS9jD334-6o6g4M9F Goodluck``` |
  | 6 | Estado original -> WARP IPv6 |
  | d | Estado original -> WARP doble pila |
  | o | Switch warp-go, juzga el estado actual y activa/desactiva automáticamente |
  | u | Desinstalar warp-go |
  | v | Sincronizar el script a la última versión |
  | Otro o vacío | Interfaz de menú |


## API de Cloudflare

### Guía de uso de la Cli-API, acceso desde el navegador con parámetros o mediante el comando `curl` para ejecutar solicitudes a la API Warp,

| Parámetro run | Descripción | Parámetros | Ejemplo |
|---|---|---|---|
|  | Guía de uso | | `https://warp.cloudflare.now.cc/` |
| `register` | Registrar nuevo dispositivo | `team_token (opcional)`, `format (opcional)` | `https://warp.cloudflare.now.cc/?run=register&team_token=<Tu-Team-Token>&format=<json\|yaml\|client\|wireguard\|warp-go\|\|clash\|xray\|sing-box\|qrencode>` |
| `device` | Obtener información detallada de un dispositivo | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=device&device_id=<Tu-Device-ID>&token=<Tu-Token>` |
| `app` | Obtener configuración del cliente | `token` | `https://warp.cloudflare.now.cc/?run=app&token=<Tu-Token>` |
| `bind` | Vincular dispositivo a cuenta | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=bind&device_id=<Tu-Device-ID>&token=<Tu-Token>` |
| `name` | Establecer nombre del dispositivo | `device_id`, `token`, `device_name` | `https://warp.cloudflare.now.cc/?run=name&device_id=<Tu-Device-ID>&token=<Tu-Token>&device_name=<Nombre-Dispositivo>` |
| `license` | Establecer licencia del dispositivo | `device_id`, `token`, `license` | `https://warp.cloudflare.now.cc/?run=license&device_id=<Tu-Device-ID>&token=<Tu-Token>&license=<Tu-Licencia>` |
| `unbind` | Desvincular dispositivo de la cuenta | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=unbind&device_id=<Tu-Device-ID>&token=<Tu-Token>` |
| `cancel` | Cancelar registro del dispositivo | `device_id`, `token` | `https://warp.cloudflare.now.cc/?run=cancel&device_id=<Tu-Device-ID>&token=<Tu-Token>` |
| `id` | Conversión de Client ID y Reserved | `convert` | `https://warp.cloudflare.now.cc/?run=id&convert=<cadena-4-char\|Num1,Num2,Num3>` |
| `token` | Obtener token de Zero Trust | `organization`, `email`, `code` | paso1: `https://warp.cloudflare.now.cc/?organization=<Tu-Organization>&email=<Tu-Email>` </br> paso2: `https://warp.cloudflare.now.cc/?organization=<Tu-Organization>&cf_appsession=<App-Session-Value>&cf_session=<Session-Value>&nonce=<Nonce-Value>&code=<Tu-Code>` |
| `key` | Generar par de claves pública y privada de WireGuard | `format (opcional)` | `https://warp.cloudflare.now.cc/?run=key&format=<json\|yaml>` |

### Uso del Script Shell-API
```
wget -N https://raw.githubusercontent.com/demianrey/Warp_script/main/api.sh && bash api.sh [opción]
```
  | [opción] Variable  | Descripción de la acción |
  | ------------- | ------------- |
  | -h/--help     | Ayuda |
  | -f/--file     | Archivo para guardar la información de registro de la cuenta, soporta api oficial, client, wgcf y warp-go. Si no se indica, ingresar device id y api token manualmente |
  | -r/--register | Registrar cuenta |
  | -t/--token    | Al registrar con -r, usar team token para registrar, acceso rápido: https://web--public--warp-team-api--coia-mfs4.code.run |
  | -d/--device   | Obtener información de registro de cuenta, incluido tráfico plus, etc. |
  | -a/--app      | Obtener información de la app |
  | -b/--bind     | Obtener información del dispositivo vinculado, incluidos sub-dispositivos |
  | -n/--name     | Modificar nombre del dispositivo |
  | -l/--license  | Modificar licencia |
  | -u/--unbind   | Desvincular dispositivo |
  | -c/--cancle   | Cancelar cuenta |
  | -i/--id       | Mostrar client id y reserved |


## Cómo obtener una IP WARP desbloqueada para Netflix

* Puedes usar otro script de un clic que desbloquea medios de streaming a través de WARP: [【Renovar IP WARP】 - Diseñado para desbloquear streaming con WARP](https://github.com/fscarmen/unlock_warp)

* Tomando Hong Kong hk como ejemplo, ejecuta `warp i`. Se recomienda ejecutar en segundo plano con screen o nohup

* Si la IP desbloqueada no aparece después de mucho tiempo, verifica si CloudFlare está en mantenimiento en tu zona: https://www.cloudflarestatus.com/


## Plantilla de enrutamiento WARP socks5 o interface y desbloqueo de chatGPT

<details>
    <summary> Plantilla de configuración Xray para enrutar sitios web hacia socks5 (para WARP Client Proxy y WireProxy) (clic para expandir o contraer)</summary>
<br>

Socks5 local: socks5://127.0.0.1:40000
Tomando el [script ocho-en-uno de mack-a](https://github.com/mack-a/v2ray-agent) como ejemplo. Edita ```/etc/v2ray-agent/xray/conf/10_ipv4_outbounds.json```

```
{
    "outbounds":[
        {
            "protocol":"freedom"
        },
        {
            "tag":"warp",
            "protocol":"socks",
            "settings":{
                "servers":[
                    {
                        "address":"127.0.0.1",
                        "port":40000 // Ingresa tu puerto socks5
                    }
                ]
            }
        },
        {
            "tag":"WARP-socks5-v4",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv4"
            },
            "proxySettings":{
                "tag":"warp"
            }
        },
        {
            "tag":"WARP-socks5-v6",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv6"
            },
            "proxySettings":{
                "tag":"warp"
            }
        }
    ],
    "routing":{
        "rules":[
            {
                "type":"field",
                "domain":[
                    "geosite:openai",
                    "ip.gs"
                ],
                "outboundTag":"WARP-socks5-v4"
            },
            {
                "type":"field",
                "domain":[
                    "geosite:google",
                    "geosite:netflix",
                    "p3terx.com"
                ],
                "outboundTag":"WARP-socks5-v6"
            }
        ]
    }
}
```
</details>

<details>
    <summary> Plantilla de configuración Xray para enrutar sitios web hacia "interface" (para WARP Client Warp y warp / warp-go no-global) (clic para expandir o contraer)</summary>
<br>

```
{
    "outbounds":[
        {
            "protocol":"freedom"
        },
        {
            "tag":"WARP-interface-v4",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv4"
            },
            "streamSettings":{
                "sockopt":{
                    "interface":"CloudflareWARP", // Para modo no-global de warp, usar warp; para modo Proxy del Client, CloudflareWARP; para warp-go, WARP
                    "tcpFastOpen":true
                }
            }
        },
        {
            "tag":"WARP-interface-v6",
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv6"
            },
            "streamSettings":{
                "sockopt":{
                    "interface":"CloudflareWARP",
                    "tcpFastOpen":true
                }
            }
        }
    ],
    "routing":{
        "domainStrategy":"AsIs",
        "rules":[
            {
                "type":"field",
                "domain":[
                    "geosite:google",
                    "geosite:openai",
                    "ip.gs"
                ],
                "outboundTag":"WARP-interface-v4"
            },
            {
                "type":"field",
                "domain":[
                    "geosite:netflix",
                    "p3terx.com"
                ],
                "outboundTag":"WARP-interface-v6"
            }
        ]
    }
}
```
</details>

<details>
    <summary> Cómo desbloquear chatGPT a través de WARP (clic para expandir o contraer)</summary>
<br>

La idea es usar el warp ya registrado para configurar un proxy encadenado. Esta solución es la más ligera y los usuarios solo necesitan xray. El método es modificar el outbound y el routing del archivo de configuración de xray. La plantilla es la siguiente:
```
{
    "outbounds":[
        {
            "protocol":"freedom",
            "tag": "direct"
        },
        {
            "protocol":"wireguard",
            "settings":{
                "secretKey":"YFYOAdbw1bKTHlNNi+aEjBM3BO7unuFC5rOkMRAz9XY=", // Pega tu valor "private_key"
                "address":[
                    "172.16.0.2/32",
                    "2606:4700:110:8a36:df92:102a:9602:fa18/128"
                ],
                "peers":[
                    {
                        "publicKey":"bmXOC+F1FxEMF9dyiK2H5/1SUtzH0JuVo51h2wPfgyo=",
                        "allowedIPs":[
                            "0.0.0.0/0",
                            "::/0"
                        ],
                        "endpoint":"engage.cloudflareclient.com:2408" // O ingresa 162.159.192.1:2408 o [2606:4700:d0::a29f:c001]:2408
                    }
                ],
                "reserved":[78, 135, 76], // Pega tu valor "reserved"
                "mtu":1280
            },
            "tag":"wireguard"
        },
        {
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv4"
            },
            "proxySettings":{
                "tag":"wireguard"
            },
            "tag":"warp-IPv4"
        },
        {
            "protocol":"freedom",
            "settings":{
                "domainStrategy":"UseIPv6"
            },
            "proxySettings":{
                "tag":"wireguard"
            },
            "tag":"warp-IPv6"
        }
    ],
    "routing":{
        "domainStrategy":"AsIs",
        "rules":[
            {
                "type":"field",
                "domain":[
                    "geosite:openai",
                    "ip.gs"
                ],
                "outboundTag":"warp-IPv4"
            },
            {
                "type":"field",
                "domain":[
                    "geosite:netflix",
                    "p3terx.com"
                ],
                "outboundTag":"warp-IPv6"
            }
        ]
    }
}
```
</details>


## Obtención de WARP+ License e ID

Lo siguiente es la introducción oficial a Argo 2.0 después de usar WARP y Team: [Argo 2.0: Smart Routing Learns New Tricks](https://blog.cloudflare.com/argo-v2/)

Cita de Luminous: Las pruebas reales muestran que WARP+ no tiene diferencia con la versión gratuita en términos de velocidad al acceder a sitios web que no son de CF. Solo al acceder a los sitios de CloudFlare, la versión de pago utilizará tecnología similar a Argo para ir al origen a través de un centro de datos más cercano al destino, mientras que la versión gratuita está limitada a ir al origen desde la ubicación de conexión, eso es todo.

<img src="https://user-images.githubusercontent.com/62703343/136070323-47f2600a-13e4-4eb0-a64d-d7eb805c28e2.png" width="70%" />


## Cómo obtener y usar WARP Teams en Linux

* https://warp-token.cloudflare.now.cc/ , a través del sitio web de fscarmen

* https://web--public--warp-team-api--coia-mfs4.code.run/, a través del sitio web de Coia

## Principio de WARP

WARP es un servicio de seguridad y aceleración del tráfico de red basado en WireGuard proporcionado por CloudFlare, que te permite lograr protección de privacidad y optimización de enlaces conectándote a los nodos perimetrales de CloudFlare.

Su punto de conexión es de doble pila (IPv4/IPv6 disponibles), y tras la conexión puedes obtener direcciones IPv4 e IPv6 basadas en NAT proporcionadas por CF. Por lo tanto, nuestro servidor de pila única puede intentar conectarse a WARP para obtener soporte adicional de conectividad de red. De esta manera, podemos permitir que los servidores con solo IPv6 accedan a IPv4, y también que los servidores con solo IPv4 obtengan capacidades de acceso IPv6.

* Agregar IPv4 a servidores con solo IPv6

Como se muestra en la figura, el tráfico IPv4 es tomado por la tarjeta de red WARP, lo que permite que el tráfico IPv4 acceda a la red externa a través de WARP.

<img src="https://user-images.githubusercontent.com/62703343/135735404-1389d022-e5c5-4eb8-9655-f9f065e3c92e.png" width="70%" />

* Agregar IPv6 a servidores con solo IPv4

Como se muestra en la figura, el tráfico IPv6 es tomado por la tarjeta de red WARP, lo que permite que el tráfico IPv6 acceda a la red externa a través de WARP.

<img src="https://user-images.githubusercontent.com/62703343/135735414-01321b0b-887e-43d6-ad68-a74db20cfe84.png" width="70%" />

* Reemplazo de red para servidores de doble pila

A veces nuestro servidor es de doble pila, pero por varias razones podemos no querer usar una de las redes. En este caso, también podemos usar WARP para tomar el control de parte de la conexión de red para ocultar nuestra dirección IP. El propósito de hacer esto, la mayor significancia es reducir la probabilidad de captchas en algunos centros de datos con mucho abuso; al mismo tiempo, algunos proveedores de contenido tratan la IP de destino de WARP como la IP nativa de usuarios reales, lo que puede levantar algunos bloqueos basados en IP.

<img src="https://user-images.githubusercontent.com/62703343/135735419-50805ed6-20ea-4440-93b4-5bcc6f2aca9b.png" width="70%" />

* Rendimiento de red: Kernel integrado > Módulo del kernel > wireguard-go


## Agradecimientos a los Contribuidores de WARP y Estado del Servicio Global de CloudFlare WARP

Internet nunca olvida, pero las personas sí.

Artículos técnicos o proyectos relacionados (sin orden particular):
* P3terx: https://p3terx.com/archives/use-cloudflare-warp-to-add-extra-ipv4-or-ipv6-network-support-to-vps-servers-for-free.html
* P3terx: https://github.com/P3TERX/warp.sh/blob/main/warp.sh
* Oreomeow: https://github.com/Oreomeow
* Luminous: https://luotianyi.vc/5252.html
* Hiram: https://hiram.wang/cloudflare-wrap-vps
* Cloudflare: https://pkg.cloudflareclient.com/
https://blog.cloudflare.com/announcing-warp-for-linux-and-proxy-mode/
https://blog.cloudflare.com/argo-v2/
* WireGuard: https://lists.zx2c4.com/pipermail/wireguard/2017-December/002201.html
* Parker C. Stephens: https://parkercs.tech/cloudflare-for-teams-wireguard-config/
* Anemone: https://cutenico.best/posts/blogs/cloudflare-warp-fixed-youtube-location/
https://github.com/acacia233/Project-WARP-Unlock
* wangying202: https://blog.csdn.net/wangying202/article/details/113178159
* LUBAN: https://github.com/HXHGTS/Cloudflare_WARP_Connect
* valetzx: https://gitlab.com/valetzx/pubfile
* badafans cf api: https://github.com/badafans/warp-reg
* chika0801: https://github.com/chika0801/Xray-examples/
* xXcmd1152Xx: https://github.com/cmd1152/WarpPlusKeyGenerator-NG-lib
* Todos los usuarios entusiastas de la red

Proveedores de servicios (sin orden particular):
* API Warp de fscarmen: https://warp.cloudflare.now.cc/
* API Zero Trust Token de fscarmen: https://warp-token.cloudflare.now.cc/
* CloudFlare Warp(+): https://1.1.1.1/
* Autor original del proyecto WGCF: https://github.com/ViRb3/wgcf/
* Coia y equipo warp-go: https://gitlab.com/ProjectWARP/warp-go
* Wiki de la API warp-go: https://docs.zeroteam.top/apis/warp
* WireGuard-GO oficial: https://git.zx2c4.com/wireguard-go/
* Trabajo maduro de ylx2016: https://github.com/ylx2016/Linux-NetSpeed
* Trabajo maduro de ALIILAPRO: https://github.com/ALIILAPRO/warp-plus-cloudflare
* Trabajo maduro de mixool: https://github.com/azples/across/tree/main/wireguard
* Trabajo maduro de luoxue-bot: https://github.com/luoxue-bot/warp_auto_change_ip
* Trabajo maduro de lmc999: https://github.com/lmc999/RegionRestrictionCheck
* Autor de WireProxy: https://github.com/pufferffish/wireproxy
* Consulta de IP pública y ubicación: https://ifconfig.co/ , https://ip.gs/ , https://ip.sb/ , https://ip-api.com
* Sitio de estadísticas PV: https://hits.seeyoufarm.com/
* Versión web de Coia para extraer Teams Token: https://web--public--warp-team-api--coia-mfs4.code.run

Estado del Sitio y Servicio Global de CloudFlare WARP:
* Operational = Normal. Re-routed = En mantenimiento: https://www.cloudflarestatus.com/
