---
title: "So baust du deine eigene Wetterstation!"
excerpt: "<br/><img src='../images/anemometer.jpg'>"
collection: projects
---

<!-- Image source for anemometer
Image by <a href="https://pixabay.com/users/ritae-19628/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3977718">-Rita-👩‍🍳 und 📷 mit ❤</a> from <a href="https://pixabay.com//?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3977718">Pixabay</a> -->

In diesem Projekt zeige ich dir, wie du mit einem Raspberry Pi Pico und einem DHT11 Sensor eine einfache Wetterstation bauen kannst. Diese Wetterstation wird in der Lage sein, Temperatur und Luftfeuchtigkeit zu messen.

- [Das brauchst du:](#das-brauchst-du)
- [Schritt 1: Hardware vorbereiten](#schritt-1-hardware-vorbereiten)
  - [1.1 Raspberry Pi Pico W vorbereiten](#11-raspberry-pi-pico-w-vorbereiten)
  - [1.2 Header-Pins anlöten](#12-header-pins-anlöten)
  - [1.3 Raspberry Pi Pico und DHT11 verbinden](#13-raspberry-pi-pico-und-dht11-verbinden)
- [Schritt 2: Software einrichten](#schritt-2-software-einrichten)
  - [2.1 Thonny IDE/Entwicklungsumgebung installieren](#21-thonny-ideentwicklungsumgebung-installieren)
  - [2.2 Benötigte Bibliotheken](#22-benötigte-bibliotheken)
- [Schritt 3: Programmierung](#schritt-3-programmierung)
  - [3.1 Code-Erklärung:](#31-code-erklärung)
  - [3.2 Skript speichern und hochladen](#32-skript-speichern-und-hochladen)
  - [3.3 Diagramm-Funtkion aktivieren](#33-diagramm-funtkion-aktivieren)
- [Nützliche Ressourcen](#nützliche-ressourcen)


## Das brauchst du:

Um deine eigene Messstation zu entwerfen, benötigst du nur wenige Bauteile. Die meisten findest du im Baumarkt oder kannst sie ganz einfach im Internet bestellen.

- Raspberry Pi Pico W (Ein Basic Kit ist z.B. [hier](https://www.amazon.de/GeeekPi-Raspberry-Pico-Basic-Kit/dp/B0BHQ8KT41/) erhältlich)
- DHT11 Sensor (ist ein digitaler Temperatur- und Luftfeuchtigkietssensor)
- Breadboard (Steckbrett)
- Jumper-Kabel
- Header-Pins (falls noch nicht auf dem Pico W angelötet)
- Lötstation oder Lötkolben (falls Header-Pins noch nicht angelötet sind)
- USB-Kabel (USB-A auf Micro-USB) zum Verbinden des Mikrocontrollers mit dem Computer
- Python und Thonny IDE

## Schritt 1: Hardware vorbereiten

### 1.1 Raspberry Pi Pico W vorbereiten

Der Raspberry Pi Pico W ist ein kleines, kostengünstiges Computer-Board. Es hat einen Mikrocontroller, der wie ein kleines Gehirn funktioniert, und es hat WLAN, damit es sich mit dem Internet verbinden kann. Du kannst es leicht programmieren, um verschiedene Aufgaben auszuführen, wie zum Beispiel unsere Wetterstation zu betreiben.

> Weitere wichtige Informationen und detaillierte Anweisungen zur Vorbereitung des Raspberry Pi Pico W findest zu auf dieser [Website](https://projects.raspberrypi.org/en/projects/get-started-pico-w/1).

### 1.2 Header-Pins anlöten

Falls dein Raspberry Pi Pico W keine vorinstallierten Header-Pins hat, löte diese zunächst an. Verwende dazu einen Lötkolben und Lötzinn. 
> Hier ist ein hilfreiches [Tutorial zum Löten](https://www.youtube.com/watch?v=R11QanPDccs).

Platziere die Header-Pins in die entsprechenden Löcher und erhitze die Pins, während zu das Lötzinn zuführst, bis die Verbindungen fest sind. (Achte darauf, dass die Pins gerade und gut verlötet sind!)

### 1.3 Raspberry Pi Pico und DHT11 verbinden

- Stecke den Raspberry Pi Pico W auf das Breadboard
- Schließe den DHT11 Sensor an
- Verbinde die Juper-Kabel wie folgt:
  - VCC des DHT11 Sensors (rotes Kabel) an 3V3(OUT) des Pico
  - GND des Sensors (schwarzes Kabel) an GND des Pico
  - SIG(Data) des Sensors (gelbes Kabel) an GP3

![Schaltplan des Aufbaus](/images/hardware-pico.png)

Verbinde anschließend den Raspberry Pi Pico W über ein USB-Kabel (Typ A auf Micro USB) mit deinem Computer. Dieses Kabel wird verwendet, um den Mikrocontroller mit Strom zu versorgen und die Kommunikation zwischen dem Mikrocontroller und deinem Computer zu ermöglichen.

![Aufbau](/images/aufbau.png)

## Schritt 2: Software einrichten

### 2.1 Thonny IDE/Entwicklungsumgebung installieren

Gehe auf die [Thonny-Website](https://thonny.org/) und lade die Installationsdatei für dein Betriebssystem herunter.
![Entwicklungsumgebung](/images/thonny-install.png)

### 2.2 Benötigte Bibliotheken

Das DHT-Modul ist bereits in der MicroPython-Firmware enthalten. Du musst also keine zusätzlichen Bibliotheken installieren.

## Schritt 3: Programmierung

Nun ist alles fertig eingerichtet und du kannst mit dem Programmieren anfangen. Erstelle ein neues Python-Skript in der Thonny IDE und füge den folgenden Code ein:

``` py
from dht import DHT11
import dht
import machine
import time

sensor = dht.DHT11(machine.Pin(3))

while True:
  sensor.measure()
  temp = sensor.temperature()
  hum = sensor.humidity()
  print('Temperatur:', temp, '°C')
  print('Luftfeuchtigkeit:', hum, '%')
  time.sleep(2)
```

### 3.1 Code-Erklärung:

- **Bibliotheken einbinden** (Die ersten 4 Zeilen): Zu Beginn werden die notwendigen Bibliotheken importiert.

- **Sensor initialisieren** (Zeile 6): Hier sagen wir der Library welchen Pin wir für den Sensor nutzen möchten (GP3).

- **while-Schleife** (Ab Zeile 8): In der Schleife wird die Messung kontinuierlich durchgeführt, die gemessenen Werte für Temperatur und Luftfeuchtigkeit ausgelesen und in der Konsole angezeigt. Die Schleife pausiert dann für 2 Sekunden, bevor die nächste Messung beginnt.

### 3.2 Skript speichern und hochladen

- Speichere das Skript und lade es auf den Raspberry Pi Pico hoch.

![Speicherort](/images/speicherort-pico.png)

- Öffne den Serial Monitor in der Thonny IDE, um die gemessenen Werte für Temperatur und Luftfeuchtigkeit anzuzeigen. 

### 3.3 Diagramm-Funtkion aktivieren

Um die gemessenen Werte grafisch anzuzeigen, kannst du in Thonny die Plotter-Funktion aktivieren. Diese Funktion zeigt die Daten in Echtzeit in einem Diagramm an.

1. Gehe in das Menü **Ansicht**
2. Aktiviere die Option **Drucken**

![Thonny](/images/thonny-drucken.png)

3. Nachdem du die Option ausgewählt hast, musst du noch die `print`-Anweisung in deinem Code wie folgt anpassen:

``` py
print('Temperatur:', temp, '°C', 'Luftfeuchtigkeit:', hum, '%')
```

Diese Anpassung sorgt dafür, dass beide Werte in einer einzigen Zeile ausgegeben werden, was vom Plotter in Thonny korrekt interpretiert wird.

![Übersicht](/images/thonny-plotter.png)

---
## Nützliche Ressourcen

- [Pinout Diagram](https://datasheets.raspberrypi.com/picow/PicoW-A4-Pinout.pdf?_gl=1*hp6qf5*_ga*MTIzMTI5MzgyOC4xNzE5MDQ1MDIz*_ga_22FD70LWDS*MTcxOTA0NTAyMy4xLjEuMTcxOTA0NTEwMS4wLjAuMA..)

- [Raspberry Pi Pico W Datasheet](https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf?_gl=1*on3s79*_ga*MTIzMTI5MzgyOC4xNzE5MDQ1MDIz*_ga_22FD70LWDS*MTcxOTA0NTAyMy4xLjEuMTcxOTA0NTExOS4wLjAuMA..)

- [Connecting to the Internet with Raspberry Pi Pico W](https://datasheets.raspberrypi.com/picow/connecting-to-the-internet-with-pico-w.pdf?_gl=1*on3s79*_ga*MTIzMTI5MzgyOC4xNzE5MDQ1MDIz*_ga_22FD70LWDS*MTcxOTA0NTAyMy4xLjEuMTcxOTA0NTExOS4wLjAuMA..)
