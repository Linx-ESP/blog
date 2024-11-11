---
date: 2024-11-11
authors: 
    - Linx
categories:
    - Gaming
tags:
    - Launchers
    - Playnite
slug: Playnite
---

# Playnite - Configuración y personalización

[Playnite](https://github.com/JosefNemec/Playnite/) es un launcher de PC que permite incorporar otras bibliotecas como Steam, Ubisoft Connect, Epic Games para poder usarlo como un launcher central.  
Cuenta también chorrocientos plugins para añadir bibliotecas, información, imagenes o funciones adicionales.

<!-- more -->

## Plataformas que uso

- Steam
    - Steam + [SteamGridDB / SRM](https://github.com/SteamGridDB/steam-rom-manager) es perfectamente capaz de actuar como launcher unificado, con el beneficio de Steam Input global
    - Se queda corto en gestionar la instalación de juegos (SRM solo importa juegos ya instalados) y en plugins para funciones adicionales o metadatos
        - Por ejemplo, metadata de terceros, guardado de partidas.
    - [Decky Loader](https://decky.xyz/) todavía no ofrece una versión estable (o usable) para Windows.
    - [Millenium](https://steambrew.app/) of    rece temas para Steam, si su sistema de plugins avanza probablemente sea mejor opción.

- Epic Games
    - [Legendary](https://github.com/derrod/legendary) es un launcher por cli compatible con partidas en la nube, overlay y más funciones.
    - [Heroic](https://heroicgameslauncher.com/) es una GUI para legendary (EGS), nile (Amazon Games) y GOG.

- GOG
    - GOG Galaxy no rinde ni ofrece las opciones que Playnite o Steam + Steam ROM Manager.
    - No parece que siga en desarrollo, y los plugins están más limitados.

- Otros
    - Amazon Games a través de Heroic / [Nile](https://github.com/imLinguin/nile)
    - Humble Bundle para Humble Vault (no que lo use)

- Emuladores (ROMs almacenadas en un NAS y gestionadas con [ROMM](https://github.com/rommapp/romm))
    - Algunos emuladores son parte de [RetroArch (Steam)](https://store.steampowered.com/app/1118310/RetroArch/)
    - Los emuladores no cuentan con almacenamiento de partidas o save states salvo RetroArch
    - No suele haber una tienda digital de la que extraer metadatos/imagenes


## Objetivos

### Automatización

No se debe requerir intervención manual para:
- Importar o actualizar juegos o DLCs.
    - Seguro que esto no tendrá consecuencias en juegos con +100GB de mapas en DLCs. _ejem, Ark_
    - Esto incluye detectar cuando los juegos se han desinstalado con el launcher de manera externa a Playnite

- Descargar imagenes y metadata.

- Sincronizar partidas con la nube o copia privada
    - [Ludusavi](https://github.com/mtkennerly/ludusavi), por suerte, incluye toda la información de los archivos de guardado de los juegos. Así que cubre los juegos de fuera de Steam y Epic

Puede requerir intervención manual:
- Instalar y desinstalar juegos, obviamente
    - No deberá ser más que un solo clic, o como mucho, seleccionar ruta de instalación (el por defecto será configurado).

- Configuración iniciales personalizadas
    - Esto incluyen configurar rutas de descarga, nombres o valores específicos o comportamientos de arranque. Será configurar a partir de los valores que ya vienen, no desde cero.

### Incorporación de emuladores

Esto incluye:
- Adquisición de metadata. 
    - No hay un proveedor de donde se pueda sacar como es en el caso de Steam o Epic que se saca la info desde la web de su tienda con todas las categorías, fechas e info adicional.
    - Las descripciones y portadas tendrán que ser MUY preferiblemente las localizadas/regionales.

- Gestión de instalación.
    - En plataformas online tienes disponibles los juegos no instalados. No es el caso de emuladores de consolas.
    - Mis juegos que no están "instalados" están almacenados en un NAS, pero para cualquier cosa que supere la 6ª/7ª generación de consolas no es viable jugar con los juegos en el NAS (con mejor red local o cachés sería más viable).
    - Por suerte mi NAS cuenta con [ROMM](https://github.com/rommapp/romm) que gestiona los juegos del NAS y ofrece un plugin en Playnite para que se muestre como biblioteca de la que descargar que mantiene compatibilidad con la gestión de emuladores de Playnite.
        - Una opción alternativa es el plugin [EmuLibrary](https://github.com/psychonic/Playnite-EmuLibrary) que no requiere más que una carpeta externa, sin instalación de programas en el NAS.

- Integración con emuladores
    - No pienso incluir las opciones de lanzamiento por cada juego, no quita que en algún momento quiera hacerlo por cosas como configuraciones personalizadas por juego (_aunque debería ser el emulador el que se encargue, como Dolphin_)

### Gestión de metadatos

Uno de los principales factores por los que no uso Steam para juegos de terceros es la falta de información de los juegos externos.   
Los juegos propios de Steam cuentan con descripciones, tiempo jugado, logros, actividad de los amigos, noticias... Los juegos externos muestran una pantalla vacía con nada más que el mensaje de que no hay información disponible porque no es un juego de Steam (no parece ni que SteamEdit pueda hacerlo).

#### ¿Cuánta información ofrece Playnite?

Gracias a plugins:

- De las integraciones de otras bibliotecas (Steam, GOG, EGS, etc): Imagenes, logros, actividad...
- Sección de noticias de Steam
- Metadatos generales desde IGDB, Steam incluso para juegos de otras bibliotecas, IGN, Wikipedia
- Para ROMs: ScreenScraper, GameTDB (Wii y GC), Nintendo Store (experimental), LaunchBox
- Info más específica: imagenes de SteamGridDB, etiquetas avanzadas de PCGW
  


## Configuración

### Configuración de playnite

=== "General"

    - Al iniciar el juego: 
        - Recomendado: minimizar
    - Después de cerrar el juego:
    - Mostrar el icono en la bandeja del sistema: 
        - Recomendado: Sí + Minimizar Playnite a la bandeja al cerrar la ventana
    - Descargar metadatos después de importar juegos
        - Recomendado: Sí, parte de la automatización
    - Iniciar en pantalla completa: modo para mandos similar a Steam Big Picture

=== "Actualizando"

    - Actualizar Bibliotecas: en cada inicio
    - Escanera carpetas de emulación: en cada inicio (en desuso con ROMM)
    - Buscar actualizaciones: una vez a la semana

=== "Metadatos"

    <div class="annotate" markdown>
    - Precargar imágenes de fondo: sí  
    - Organización calificación por edad: PEGI (PEGI=EU, ESRB=NA)  
    - Proveedores  
        - Regla general:  
            - *Imagenes:* Steam → SteamGridDB → ScreenScraper(1) → IGDB(2).  
            - *Info:* Steam (salvo fecha lanzamiento)(3) → PCGW → ScreenScraper(1) → IGDB(2).  
    </div>

    1.  Para ROMs de consolas, ya que no podrá adquirirlo de otro lado, excepto SteamGrid que está bien
    2.  IGDB y bases de datos generales que cuentan con información más pobre pero sobre más títulos
    3.  La fecha de lanzamiento en Steam no tiene que coincidir con el lanzamiento en PC (juegos de Ubi) o al mercado (juego multiplataforma) 

=== "Adicional"
    - Cerrar automáticamente clientes
        - El retraso del cierre tiene que ser suficiente como para sincronizar con la nube. Steam por su tamaño y funciones como la de los mandos quizás es mejor no cerrarlo
    - Copia de seguridad, porque no tendrás ganas de configurar esto otra vez. 
        - La parte de media es la que más ocupa y normalmente se puede recuperar, pero se perderían imagenes personalizadas.
    - Avanzado
        - Discord Rich Presence: Compartir en discord a que estás jugando (los juegos o emuladores toman prioridad con su propio Rich Presence)

### Complementos

#### Bibliotecas

Salvo Xbox, querrás marcar la opción de importar juegos no instalados para poder instalarlos desde Playnite.

- Amazon Games: marcar "Iniciar directamente sin el cliente oficial"
- Battle.net, EA, Ubisoft requieren el launcher oficial instalado.
- GoG detecta juegos instalados de manera externa a Playnite sin necesidad de GOG Galaxy
- Xbox, desmarcar "Importar juegos no instalados" salvo que quieras manualmente quitar todos los juegos de Game Pass **que hayas jugado al menos una vez** 
- Steam incluye la opción de importar metadatos 
- Minecraft: Usar MultiMC/Poly/Prism y [Prism Launcher](https://prismlauncher.org/) en vez del oficial
- RomM en caso de que uses RomM, o EmuLibrary si tus roms están en otra ubicación como un NAS

#### Fuentes de metadatos

- Custom Steam Covers: si tienes imagenes personalizadas en Steam (de Steam ROM Manager o SteamGridDB por ejemplo)
    - Si es el caso, querrás darle máxima prioridad en la configuración de metadatos
- IGDB como fuente de metadatos en caso de que nada más lo detecte
- PCGamingWiki para etiquetas como HDR, ultrawide, Dualshock, detalles de otras funciones o enlaces a webs externas
- ScreenScraper es una web por voluntarios que sirve de proveedor de metadatos e imágenes para juegos de consolas
- Steam Store Provider, porque si no solo se puede añadir información de Steam a los juego que se importe a través de Steam
- [SteamGridDB](https://www.steamgriddb.com/), proveedor de imagenes tanto "oficiales" como personalizadas creadas por la gente. Ver su web.

#### Genérica

Hay muchas más de las que puedo explicar, unas recomendaciones son:

- Duplicate Hider: Para combinar juegos que tengas en varias plataformas como una sola entrada, unificar metadata y priorizar que versión o launcher usar. Lo hace automáticamente pero permite añadir grupos manualmente.
- Extrametadata Loader: En temas que lo soporten mostrará los logos de los juego o trailers/videos cortos. Sobre todo por los logos que saca de SteamGrid.
- [HowLongToBeat](https://howlongtobeat.com/): incluye una gráfica con info de HLTB
- Ludusavi, que si se instala permite hacer copias de las partidas guardadas. Útil como copia adicional en la nube o para launchers que no lo soporte, o con algo de mano, de emuladores.
- Steam News y player count
- Steam Store Screenshots Viewer
- SuccessStory: logros de más plataformas que Steam.

#### Temas

Yo uso FusionX o Helium para escritorio y Anthem o Hero para pantala completa (similar al modo Big Picture)