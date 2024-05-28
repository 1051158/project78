# project78
# Inhoudsopgave
- [Project78](#project78)
  - [Stream](#stream)
    - [Beschrijving](#beschrijving)
    - [Vereisten](#vereisten)
    - [Dependencies](#dependencies)
    - [Installatie](#installatie)
    - [Compilatie](#compilatie)
    - [Gebruik](#gebruik)
    - [Functies](#functies)
    - [Voorbeeld](#voorbeeld)
    - [FIFO-pijpen](#fifo-pijpen)

## Stream
### Beschrijving
Deze toepassing streamt video van een camera naar een specifieke host en poort via RTP, met de mogelijkheid om de bitrate en kleurmodus aan te passen via FIFO-pijpen.

### Vereisten
- GStreamer 1.0
- GLib
- g++ compiler

### Dependencies
Zorg ervoor dat de volgende bibliotheken zijn geïnstalleerd:
- `gstreamer-1.0`
- `glib-2.0`

### Installatie
Installeer de vereiste pakketten op Ubuntu via de volgende opdrachten:
```sh
sudo apt-get update
sudo apt-get install gstreamer1.0-tools gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly libglib2.0-dev g++
```
### Compilatie
```sh
g++ -std=c++11 stream.cpp -o stream `pkg-config --cflags --libs gstreamer-1.0`
```

### Gebruik
Start de toepassing met
```sh
./stream <IP_ADRES> <POORT> <BITRATE>
```
waar:
- `<IP_ADRES>` het IP-adres van de host is waarnaar gestreamd wordt.
- `<POORT>` de poort is waarop gestreamd wordt.
- `<BITRATE>` de initiële bitrate in kbps is.

### Functies
- Bitrate aanpassen: De bitrate kan worden aangepast door een nieuwe waarde naar /tmp/bitrate_fifo te schrijven.
- Kleurmodus wisselen: De kleurmodus (kleur of grijswaarden) kan worden gewisseld door color of greyscale naar /tmp/color_toggle_fifo te schrijven.

### Voorbeeld
Stel, je wilt streamen naar IP-adres 192.168.1.100 op poort 5000 met een initiële bitrate van 500 kbps:
```sh
./stream 192.168.1.100 5000 500
```

### FIFO-pijpen
Als je het standalone gebruikt, zorg ervoor dat de FIFO-pijpen zijn gemaakt voordat je de toepassing start:
```sh
mkfifo /tmp/bitrate_fifo
mkfifo /tmp/color_toggle_fifo
```
