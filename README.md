![Banner](https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Banner_GitHub_Feb2023.png?raw=true)
[![Öffnen in Colab](https://img.shields.io/badge/Open%20in%20Colab-grey?style=flat-square&logo=google-colab&logoColor=F9AB00&labelColor=grey&color=F9AB00)](https://colab.research.google.com/drive/1halSc73m1BsovgJhM2FQkquQVUpD2_7B?usp=sharing)


Willkommen auf der GitHub Seite zu meiner **Bachelorarbeit**:  
**Entwicklung einer KI-basierten Objekterkennungsapplikation für einen Industrieroboter**.  

---

## 🎯 Projektübersicht

In meiner Bachelorarbeit habe ich ein YOLOv8s-Modell trainiert, das speziell für die Objekterkennung von Bauklötzen entwickelt wurde und auf dem Raspberry Pi 5 mit dem AI Kit sowie der Camera Module 3 ausführbar ist.

Diese GitHub-Seite bietet:
- **Zugriff auf wichtige Dokumente, Codes und Ergebnisse**, um die Arbeit für Leser und Nutzer nachvollziehbar zu machen.
- **Detaillierte Repositories**, die Aspekte wie Modelltraining und Datensatzaufbereitung beleuchten.
---

### 📂 Schritte der Projektumsetzung

1. Erstellen eines benutzerdefinierten Datensatzes mit Roboflow
2. Trainieren des Modells und Validierung der Ergebnisse
3. Ausführen des Modells auf dem Raspberry Pi 5
4. Konvertieren des Modells in das ONNX-Format
5. Konvertieren des ONNX-Modells in das HEF-Format
6. Ausführen des konvertierten Modells auf dem Raspberry Pi 5 & AI Kit
   
Diese Schritte umfassen den gesamten Entwicklungsprozess – von der Datensammlung über das Modelltraining bis hin zur finalen Anwendung auf der Hardware. Im Folgenden wird auf jede Projektphase detailliert eingegangen, um die Umsetzung und die verwendeten Methoden näher zu erläutern.

---

## 📸 Erstellen eines benutzerdefinierten Datensatzes mit Roboflow
[Roboflow](https://roboflow.com/) bietet eine übersichtliche Plattform zur Erstellung, Annotation (Abgrenzungen von Objekten in Bildern) und Verwaltung von Datensätzen. Mit über 110.000 öffentlich zugänglichen Datensätzen in [Roboflow Universe](https://universe.roboflow.com/) ist es ein vielseitiges Werkzeug für verschiedene Anwendungsbereiche. 

Im Folgenden wird gezeigt, wie ein benutzerdefinierter Datensatz erstellt werden kann.


### Schritt 1: Projekt erstellen:
Zum Erstellen eines neuen Projekts ist die [Registrierung bei Roboflow](https://app.roboflow.com/login) erforderlich. Nach der Registrierung kann ein Workspace benannt und ein neues Projekt im Dashboard angelegt werden. Die kostenlose Variante des Public Plans ist hierfür ausreichend:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(10).gif?raw=true" alt="Demo" width="600">

### Schritt 2: Bilder hochladen:
Bilder können in das neu erstellte Projekt hochgeladen werden.
**Hinweis**: Falls ein Datensatz bereits annotierte Dateien enthält, können diese in Roboflow hochgeladen werden, wo sie automatisch erkannt und den entsprechenden Bildern zugeordnet werden:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(6).gif?raw=true" alt="Demo" width="600">


### Schritt 3: Labeln & Annotation:

- **Manuelles Annotieren:**
Diese Methode bietet maximale Kontrolle über die Präzision der Annotationen. Objekte können im Bild markiert und mit passenden Labels versehen werden. Allerdings ist dieser Prozess zeitaufwendig:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(3).gif?raw=true" alt="Demo" width="600">

- **Auto-Labeling:**
Die Auto-Labeling-Funktion automatisiert den Annotierungsprozess, indem sie nach einem kurzen begleiteten Training, bei dem das Objekt der KI beschrieben wird, die Objekte im Bild erkennt und den restlichen Datensatz automatisch labelt. Diese Funktion ist besonders hilfreich, um Zeit zu sparen. Automatisch generierte Labels können dann überprüft und bei Bedarf angepasst werden:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(9).gif?raw=true" alt="Demo" width="600">

**Hinweis**: Nach dem Labeln und Annotieren wird die Aufteilung des Datensatzes in die drei Kategorien train, test und val abgefragt. Diese Trennung sollte bestätigt werden, da sie für das spätere Modelltraining von Bedeutung ist.

### Schritt 4: Neue Datensatzversion erstellen
Nach Abschluss der Annotationen kann eine neue Version des Datensatzes generiert werden. YOLO-Modelle werden in einem quadratischen Bildformat trainiert, weshalb der Datensatz in dieser Arbeit auf die Bildgröße 640x640 skaliert wurde. Zusätzlich können Augmentationsmethoden wie Drehen, Skalieren oder das Anpassen von Helligkeit, Kontrast und Sättigung genutzt werden, um die Datenvielfalt und -robustheit zu erhöhen.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(5).gif?raw=true" alt="Demo" width="600">

### Schritt 5: Datensatz exportieren
Der Datensatz steht nach der Generierung in verschiedenen Formaten, darunter im YOLOv8-Format, zum Export bereit. Der Datensatz sollte lokal auf dem Rechner gespeichert werden, da er für die spätere Konvertierung benötigt wird, der Export kann auch über die API direkt in eine Trainingsumgebung wie Google Colab integriert werden

Im Beispiel wird gezeigt, wie mein finaler Datensatz, der für diese Arbeit erstellt wurde, in [Roboflow Universe](https://universe.roboflow.com/) gefunden und heruntergeladen werden kann.
Der Datensatz ist ebenfalls über folgenden [Direktlink](https://www.google.com/url?q=https%3A%2F%2Funiverse.roboflow.com%2Fbauklotz%2Fbauklotz-c8zsq%2Fdataset%2F1) einsehbar:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(11).gif?raw=true" alt="Demo" width="600">

✔ **Hinweis**: Nach dem Export wird empfohlen, den Datensatz erneut zu importieren, um automatisch generierte Annotationen zu überprüfen und bei Bedarf anzupassen.

---

## 2. **Trainieren des Modells und Validierung der Ergebnisse**

Das Modelltraining wird in [Google Colab](https://colab.research.google.com/drive/1halSc73m1BsovgJhM2FQkquQVUpD2_7B?usp=sharing) durchgeführt, um die Datei **best.pt** zu generieren. Dabei handelt es sich um eine PyTorch-Datei, die die optimierte Version des trainierten Modells enthält und als Basis für die Modellausführung auf dem Raspberry Pi 5 verwendet wird. Über [diesen Link](https://colab.research.google.com/drive/1halSc73m1BsovgJhM2FQkquQVUpD2_7B?usp=sharing) kann das Modelltraining in Google Colab ausgeführt werden.

---

## 3. **Ausführen des Modells auf dem Raspberry Pi 5**
#### Übertragen der Modell-Datei
Nach Erhalt der Datei **best.pt** kann diese über Google Drive auf den Raspberry Pi 5 heruntergeladen werden.

#### Einrichten der virtuellen Umgebung
Für die Modellausführung ist zunächst eine virtuelle Umgebung erforderlich. Diese isoliert das Projekt, sodass es unabhängig vom restlichen Betriebssystem und anderen installierten Paketen ausgeführt werden kann, ohne die Stabilität des Systems zu gefährden.

Mit folgendem Befehl wird eine neue virtuelle Umgebung namens **env** erstellt. Die Option **--system-site-packages** stellt sicher, dass die Umgebung Zugriff auf global installierte Python-Pakete hat:

```bash
python3 -m venv --system-site-packages env
```
```bash
source env/bin/activate
```

#### Systemaktualisierung und Paketinstallation
Das System wird aktualisiert, um sicherzustellen, dass die neuesten Paketlisten verfügbar sind und zukünftige Installationen reibungslos verlaufen. Zusätzlich wird der Python-Paketmanager installiert und auf die neueste Version aktualisiert, um die Kompatibilität mit modernen Bibliotheken zu gewährleisten:

```bash
sudo apt update
sudo apt install python3-pip -y
pip install -U pip
```

#### Installation der YOLOv8-Bibliothek
Die YOLOv8-Bibliothek von Ultralytics wird zusammen mit allen für den Export erforderlichen Paketen installiert. Dies ermöglicht die Durchführung der Objekterkennung mit YOLO auf dem Raspberry Pi:

```bash
pip install ultralytics[export]
```
#### Systemneustart

Ein Neustart des Systems stellt sicher, dass alle vorgenommenen Änderungen und Installationen übernommen wurden:

```bash
sudo reboot
```
### Nutzung von Thonny
Thonny ist eine benutzerfreundliche Entwicklungsumgebung für Python, die sich ideal für Projekte wie die Objekterkennung mit YOLO auf dem Raspberry Pi eignet. Sie ermöglicht das Arbeiten in virtuellen Umgebungen (venv), wodurch Skripte sicher getestet und ausgeführt werden können, ohne das Hauptsystem des Raspberry Pi zu beeinträchtigen. Dies erleichtert die Entwicklung direkt auf der Plattform. 

Innerhalb von Thonny kann die entsprechende virtuelle Umgebung auswählt erden.
Dadurch bleiben alle Skripte und Pakete des Projekts in der isolierten Umgebung und beeinflussen nicht das globale System.

Im folgenden Video wird gezeigt, wie die Verknüpfung von Thonny mit der venv eingerichtet wird:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20%26%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(12).gif?raw=true" alt="Demo" width="600">

#### Speicherort der virtuellen Umgebung und Ausführung des Modells

Der Ordner der virtuellen Umgebung (venv) wird standardmäßig im aktuellen Arbeitsverzeichnis erstellt, in dem der entsprechende Befehl ausgeführt wurde. Auf dem Raspberry Pi befindet sich dieses Verzeichnis in der Regel im Home-Verzeichnis des Benutzers, beispielsweise unter **/home/robolab/**. Wird die virtuelle Umgebung mit dem Namen **env** erstellt, liegt diese anschließend im Home-Verzeichnis unter **/home/robolab/env**, sofern kein alternatives Verzeichnis angegeben wurde.

Das folgende Skript sollte in die Benutzeroberfläche von Thonny eingefügt werden. Es dient der Ausführung des Modells (**best.pt**), das zuvor im Ordner der virtuellen Umgebung gespeichert wurde:


```python
import cv2
from picamera2 import Picamera2
from ultralytics import YOLO

# Kamera mit Picamera2 einrichten
picam2 = Picamera2()

# Bildgröße und Format angeben (Größe kann hier angepasst werden, z. B. (800, 800))
picam2.preview_configuration.main.size = (800, 800)
picam2.preview_configuration.main.format = "RGB888"
picam2.preview_configuration.align()
picam2.configure("preview")
picam2.start()

# YOLOv8s-Modell laden
model = YOLO("best.pt")  # Enable YOLO's default logging

# Klassennamen definieren
class_names = {0: "Bauklotz"}  # Verknüpft Klassenindizes mit Klassennamen

while True:
    # Einzelbild von der Kamera erfassen
    frame = picam2.capture_array()
    
    # YOLO-Modell auf das erfasste Bild anwenden und Ergebnisse speichern
    results = model(frame)
    detections = results[0].boxes.xyxy  # Extrahiere Koordinaten der Begrenzungsrahmen
    classes = results[0].boxes.cls     # Extrahiere Klassenindizes
    confidences = results[0].boxes.conf  # Extrahiere Konfidenzwerte

    # Zusätzliche Erkennungsdetails mit Koordinaten ausgeben
    print("\nAdditional Detection Details (with Coordinates):")
    for i, box in enumerate(detections):
        x1, y1, x2, y2 = map(int, box)  # Koordinaten als absolute Pixelwerte
        class_index = int(classes[i])
        class_name = class_names.get(class_index, "Unknown") # Klassennamen anhand des Index abrufen
        confidence = confidences[i] # Konfidenzwert für die aktuelle Erkennung

        # Erkennungsdetails ausgeben
        print(f"Object {i+1}: {class_name}, Confidence: {confidence:.2f}, Coordinates: ({x1}, {y1}, {x2}, {y2})")

        # Bounding  Box und Labels auf das Bild zeichnen
        label = f"{class_name} {confidence:.2f}"  # Klasse und Konfidenz anzeigen
        cv2.rectangle(frame, (x1, y1), (x2, y2), (0, 255, 0), 2)  # Bounding box (Begrenzungsrahmen)

        # Größe des Labels anpassen für bessere Lesbarkeit
        cv2.putText(frame, label, (x1, y1 - 10), cv2.FONT_HERSHEY_SIMPLEX, 1.0, (255, 255, 255), 2, cv2.LINE_AA)

    # Bild mit den Ergebnissen anzeigen
    cv2.imshow("Camera", frame)

    # Programm beenden, wenn "q" gedrückt wird
    if cv2.waitKey(1) == ord("q"):
        break

# Alle Fenster schließen
cv2.destroyAllWindows()
```
Das folgende Bild zeigt die Ausgabe meines trainierten Modells. Die Objekte wurden erfolgreich erkannt und mit Bounding Boxen, Klassennamen sowie Konfidenzwerten versehen.


![image](https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/PT_modell.png?raw=true)



---

## 4. **Konvertieren des Modells in das ONNX-Format**

Das **ONNX-Format** (Open Neural Network Exchange) ist ein standardisiertes Austauschformat für neuronale Netzwerke, das die plattformübergreifende Nutzung von Modellen ermöglicht. Es erlaubt den Export von Modellen aus Frameworks wie PyTorch oder TensorFlow und deren Verwendung in anderen Umgebungen.

Für die Konvertierung ist die Definition einer **Opset-Version** (Operations Set) erforderlich. Opset legt fest, welche Funktionen und Operatoren innerhalb des Modells genutzt werden können. In dieser Arbeit wurde **Opset 9** verwendet, da es stabil und weit verbreitet ist sowie mit der HEF-Pipeline von Hailo kompatibel.

Die Konvertierung in das ONNX-Format erfolgt über die YOLO CLI der Ultralytics-Pakete mit folgendem Befehl:

```bash
cd env
yolo export model=best.pt imgsz=640 format=onnx opset=9
```
Nach der erfolgreichen Ausführung wird die ONNX-Datei im Arbeitsverzeichnis der virtuellen Umgebung gespeichert. Die Ausgabe der Konsole bestätigt die erfolgreiche Konvertierung.

![Image](https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20%26%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/onnx_conversion.png)

---
## 5. **Konvertieren des ONNX-Modells in das HEF-Format**

### Einrichtung einer Linux-Umgebung mit WSL und Ubuntu 22.04

Für die Ausführung eines trainierten Modells auf dem Raspberry Pi AI Kit mit der Hailo-Hardware ist eine Konvertierung des Modells in das **Hailo Execution Format** (HEF) erforderlich. Da die Hailo-Software ausschließlich auf x86-Linux-Systemen unterstützt wird, bietet die Nutzung von **Windows Subsystem for Linux** (WSL) eine einfache Lösung für Windows-Nutzer.

Die Nutzung von WSL ermöglicht es, eine Linux-Umgebung direkt unter Windows einzurichten. Dies bietet die Vorteile einer isolierten Arbeitsumgebung und eines nahtlosen Übergangs zwischen beiden Betriebssystemen. Die Ubuntu 22.04-Distribution kann entweder über den Microsoft Store heruntergeladen oder direkt in der PowerShell installiert und verwendet werden.

<img src="https://github.com/user-attachments/assets/89f280d0-903b-4719-9b9d-d328ea8e20bd"  width="400">

#### Schritte zur Einrichtung der Linux-Umgebung:

#### 1. PowerShell öffnen:
Die PowerShell auf dem Windows-System starten, um die notwendigen Befehle auszuführen.

#### 2. Verfügbare Linux-Distributionen anzeigen:
Der folgende Befehl zeigt eine Liste der verfügbaren Linux-Distributionen an:

```powershell
wsl --list --online
```

#### 3. Ubuntu 22.04 installieren:

Die gewünschte Linux-Distribution (hier Ubuntu 22.04) wird mit folgendem Befehl installiert:


```powershell
wsl --install -d Ubuntu-22.04
```

#### 4. Benutzername und Passwort festlegen:
Während des Installationsprozesses wird ein Benutzername und ein Passwort für die zukünftige Verwendung mit **"sudo"**-Befehlen benötigt.

#### 5. System aktualisieren:
Die Paketlisten werden aktualisiert und ein System-Upgrade durchgeführt, um sicherzustellen, dass alle Pakete auf dem neuesten Stand sind:

```powershell
sudo apt update
```
```powershell
sudo apt upgrade
```

#### Hinweise:

- Das Präfix **sudo** (Superuser Do) ermöglicht die Ausführung von Befehlen mit Administratorrechten. Dies ist erforderlich, um Änderungen am System vorzunehmen.

- Nach der Installation und Einrichtung von Ubuntu wurde die Applikation genutzt, um die weiteren Schritte der Modellkonvertierung und Vorbereitung durchzuführen.


### 2. Hailo Data Compiler herunterladen 

Der Hailo Dataflow Compiler wird benötigt, um ONNX-Modelle in das HEF-Format (Hailo Execution Format) zu konvertieren, das für die Hailo-Hardware optimiert ist. Er passt Modelle an die Hardwarearchitektur an und ermöglicht durch Optimierungen wie Quantisierung eine maximale Leistung bei minimalem Ressourcenverbrauch.

#### Erforderliche Python-Pakete installieren
Die folgenden Befehle installieren die notwendigen Python-Pakete, die für den Hailo Data Compiler benötigt werden:

```bash
sudo apt install python3-pip
sudo apt install python3.10-venv
sudo apt-get install python3.10-dev python3.10-distutils python3-tk libfuse2 graphviz libgraphviz-dev
sudo pip install pygraphviz
sudo apt install wslu
```
#### Virtuelle Umgebung erstellen
Erstellen und aktivieren einer virtuellen Umgebung mit dem Namen **hailodfc**:

```bash
python3 -m venv hailodfc
source hailodfc/bin/activate
```
#### Python-Version überprüfen
Die Python-Version der Umgebung sollte 3.10.12 sein, um die Kompatibilität sicherzustellen:
Um die Kompalität mit der python Umgebung u sehen - Sie sollte 3.10.12 sein.

```bash
python3 --version
```
#### Hailo Dataflow Compiler herunterladen
Für den Download des **Hailo Dataflow Compilers** ist eine [Registrierung in der Hailo Developer Zone](https://hailo.ai/authorization/?redirect_to=https%3A%2F%2Fhailo.ai%2Fdeveloper-zone%2Fsoftware-downloads%2) erforderlich. Für die Konvertierung des Modells muss der Hailo Dataflow Compiler in der Version 3.28 heruntergeladen werden, da diese Version mit Python 3.10 kompatibel ist und die Anforderungen der Hailo-Hardware erfüllt.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(13).gif?raw=true" alt="Demo" width="600">

#### Datei in das Ubuntu-Verzeichnis verschieben
Die heruntergeladene HDC Datei sollte in das **Home-Verzeichnis** des Ubuntu-Umfelds kopiert werden. Mit folgendem Befehl wird das Zielverzeichnis geöffnet, um die Datei aus dem **Downloads-Ordner** zu verschieben:

```bash
wslview .
```

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/dataflower.jpeg?raw=true"  width="400">

#### Installation starten
Nach dem Verschieben der Datei kann die Installation des Compilers mit folgendem Befehl gestartet werden:

```bash
pip3 install hailo_dataflow_compiler-3.28.0-py3-none-linux_x86_64.whl
```
#### Installation überprüfen
Der Befehl **-h** zeigt nach erfolgreicher Installation eine Übersicht der verfügbaren Optionen und Befehle, die mit der Hailo-CLI ausgeführt werden können.

```bash
hailo -h
```
![image](https://github.com/user-attachments/assets/990df005-46d5-4626-979c-c5db122b57f1)


### 3. Hailo Model Zoo herunterladen

Der **Hailo Model Zoo** spielt eine zentrale Rolle im Workflow für die Konvertierung von Modellen in das Hailo Execution Format (HEF). Er enthält eine Sammlung vorgefertigter Modelle und Skripte, die speziell für die Hailo-Hardware optimiert sind. Diese Ressourcen ermöglichen es, Modelle effizient anzupassen, zu konvertieren und für die Ausführung auf der Hailo-Hardware vorzubereiten.

Um den Hailo Model Zoo herunterzuladen, wird das offizielle **GitHub-Repository** von Hailo verwendet:

```bash
git clone https://github.com/hailo-ai/hailo_model_zoo.git
```

Nach dem Herunterladen muss in das entsprechende Verzeichnis gewechselt werden, um die darin enthaltenen Pakete zu installieren, die für das Setup und die Konvertierung erforderlich sind:

```bash
cd hailo_model_zoo; pip install -e .

```

## 5. Vorbereitung auf die HEF Konverterierung 

Um die HEF-Konvertierung vorzubereiten, müssen mehrere Dateien und Skripte angepasst und in das richtige Verzeichnis verschoben werden. Hier eine Übersicht der erforderlichen Schritte:

### 1. best.onnx Datei übertragen

Die zuvor generierte **best.onnx**-Datei wird vom Raspberry Pi über Google Drive heruntergeladen und anschließend in das Home-Verzeichnis von Ubuntu verschoben.  Dieser Schritt stellt sicher, dass alle benötigten Ressourcen an einem Ort für die Konvertierung bereitstehen:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/best.jpeg?raw=true"  width="500">

### 2. Datensatz vorbereiten
Beim Herunterladen des Datensatzes wurden Bilder und Annotationen in drei Ordner unterteilt: **train**, **val** und **test**. Der train-Ordner muss ebenfalls in das Ubuntu-Umfeld übertragen werden, um für die Konvertierung verfügbar zu sein:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/trsin_folder.jpeg?raw=true" width="400">

### 3. Konfigurationsdateien im Hailo Model Zoo anpassen
Viele machen den Fehler, bereits jetzt den Befehl zur Performance-Optimierung auszuführen, ohne sicherzustellen, dass alle Konfigurationsdateien korrekt angepasst sind. 

Es müssen folgende Skripte erst angepasst werden:

#### a.) yolov8s.yaml
Diese Datei ist eine zentrale Konfigurationsdatei des Hailo Model Zoo und definiert alle Parameter für das Parsing, die Optimierung und die Kompilierung des Modells. Sie befindet sich im Verzeichnis: **Ubuntu-22.04 > home > irep > hailo_model_zoo > cfg > networks.**

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/network.jpeg?raw=true" width="500">

In der Konfigurationsdatei **yolov8s.yaml** sind die folgenden Änderungen vorzunehmen. Kommentare im Code weisen auf die anzupassenden Parameter hin, um die Konfiguration auf die Projektanforderungen abzustimmen:

```yaml
base:
- base/yolov8.yaml
postprocessing:
  device_pre_post_layers:
    nms: true
  hpp: true
network:
  network_name: yolov8s
paths:
  network_path:
  - best.onnx #Hier muss der genaue Pfad zur ONNX Datei angegeben werden 
  alls_script: hailo_model_zoo/hailo_model_zoo/cfg/alls/yolov8s.alls #Pfad zur ONNX-Datei angeben, die im vorherigen Schritt generiert wurde.

  url: #URL leer stehen lassen
parser:
  nodes:
  - null
  - - /model.22/cv2.0/cv2.0.2/Conv
    - /model.22/cv3.0/cv3.0.2/Conv
    - /model.22/cv2.1/cv2.1.2/Conv
    - /model.22/cv3.1/cv3.1.2/Conv
    - /model.22/cv2.2/cv2.2.2/Conv
    - /model.22/cv3.2/cv3.2.2/Conv
info:
  task: object detection
  input_shape: 640x640x3
  output_shape: 1x5x100 #Die erste Zahl gibt die Anzahl der erkannten Klassen an (1=Bauklotz).
  operations: 28.4G # GFLOPS entspricht der Angabe in der "Model Summary (fused)" aus dem Modelltraining in Google Colab
  parameters: 11.125M # Parameteranzahl basierend auf der 'Model Summary (fused)' aus Google Colab
  framework: pytorch
  training_data: coco train2017
  validation_data: coco val2017
  eval_metric: mAP
  full_precision_result: 44.75
  source: https://github.com/ultralytics/ultralytics
  license_url: https://github.com/ultralytics/ultralytics/blob/main/LICENSE
  license_name: GPL-3.0

```
Die **Parameteranzahl** und die **GFLOPS** (Giga Floating Point Operations per Second) des Modells können direkt aus den Ergebnissen des Modelltrainings in Google Colab abgelesen werden:

![image](https://github.com/user-attachments/assets/28d0eb7f-9862-49c5-9f83-c0ae7ab9c664)



### b.) yolov8s.alls

definiert spezifische Parameter und Einstellungen für die Optimierung und Konvertierung des Modells, einschließlich der Aktivierungsfunktionen (z. B. Sigmoid).
Speicherort: **Ubuntu-22.04 > home > irep > hailo_model_zoo > cfg > alls > generic.**

![image](https://github.com/user-attachments/assets/2905ce2d-8423-4528-ace4-11579f15bf11)

In der Konfigurationsdatei **yolov8s.alls** sind die folgenden Änderungen vorzunehmen. Kommentare im Code weisen auf die anzupassenden Parameter hin, um die Konfiguration auf die Projektanforderungen abzustimmen:

```plaintext
quantization_param([conv42, conv53, conv63], force_range_out=[0.0, 1.0]) #Diese Zeile ergänzen, um die Quantisierung auf die angegebenen Layer anzuwenden.
normalization1 = normalization([0.0, 0.0, 0.0], [255.0, 255.0, 255.0])
change_output_activation(conv42, sigmoid)
change_output_activation(conv53, sigmoid)
change_output_activation(conv63, sigmoid)
performance_param(compiler_optimization_level=max) #Zeile ergänzen
nms_postprocess("../../postprocess_config/yolov8s_nms_config.json", meta_arch=yolov8, engine=cpu) # Pfad zur yolov8s_nms_config.json überprüfen, um das Post-Processing korrekt zu konfigurieren.“
```

#### c.) yolov8s_nms_config.json

Die yolov8s_nms_config.json-Datei legt die Parameter für das NMS (Non-Maximum Suppression)-Postprocessing fest. Sie wird vom Dataflow Compiler genutzt, um die Nachbearbeitungsschritte für das Netzwerk zu konfigurieren. Während die voreingestellten Werte für viele Netzwerke geeignet sind, ist eine Anpassung notwendig, wenn sich Hyperparameter ändern. Speicherort: **Ubuntu-22.04 > home > irep > hailo_model_zoo > cfg > postprocess_config**

![image](https://github.com/user-attachments/assets/4172ebb3-c527-4208-8819-20472d413967)

In der Konfigurationsdatei **yolov8s_nms_config.json** sind die folgenden Änderungen vorzunehmen:

- **"image_dims": [640, 640]** // Bilddimensionen an die Trainingsparameter des Modells anpassen 
- **"classes": 1** // Klassenanzahl entsprechend des eigenen Modells anpassen (hier: 1 für Bauklotz)


```json
{
	"nms_scores_th": 0.2,
	"nms_iou_th": 0.7,
	"image_dims": [
		640,
		640 
	],
	"max_proposals_per_class": 100,
	"classes": 1, 
	"regression_length": 16,
	"background_removal": false,
	"background_removal_index": 0,
	"bbox_decoders": [
		{
			"name": "bbox_decoder41",
			"stride": 8,
			"reg_layer": "conv41",
			"cls_layer": "conv42"
		},
		{
			"name": "bbox_decoder52",
			"stride": 16,
			"reg_layer": "conv52",
			"cls_layer": "conv53"
		},
		{
			"name": "bbox_decoder62",
			"stride": 32,
			"reg_layer": "conv62",
			"cls_layer": "conv63"
		}
	]
}
```


Dieser Befehl startet die Optimierung. **Hinweis:** Die Optimierung ist zeitaufwändig und kann je nach Leistung des Systems bis zu vier Stunden dauern.

```bash
hailomz compile yolov8s --ckpt=best.onnx --hw-arch hailo8l --calib-path train/images --classes 1 --performance
```
Nach erfolgreicher Optimierung wird die HEF-Datei im angegebenen Verzeichnis gespeichert.
![image](https://github.com/user-attachments/assets/7183d63d-2382-4a96-a527-8c46464e1d64)

---
## 6. **Modellausführung auf dem Raspberry PI 5 & Ai KIT**

Zum Ausführen des Modells muss zunächst die geeignete Umgebung eingerichtet werden. Hierfür wird das Hailo-rpi5-Examples-Repository auf den Raspberry Pi heruntergeladen.

```bash
git clone https://github.com/hailo-ai/hailo-rpi5-examples.git
```
```bash
cd hailo-rpi5-examples
```
```bash
./install.sh
```
Sollte das Skript **./install.sh** nicht wie vorgesehen funktionieren, gibt es eine alternative Möglichkeit, die benötigten Pakete herunterzuladen. Hierbei wird die virtuelle Umgebung (venv) manuell eingerichtet:

```bash
source setup_env.sh
```
```bash
pip install -r requirements.txt
```
```bash
./download_resources.sh
```
```bash
./compile_postprocess.sh
```

Nach dem Schließen der virtuellen Umgebung muss für eine neue Terminalsitzung mit den installierten Paketen stets das Skript **source setup_env.sh** ausgeführt werden.

**Hinweis:** Das Verzeichnis **hailo-rpi5-examples** muss vor der Ausführung als aktuelles Arbeitsverzeichnis gesetzt sein.

```bash
cd hailo-rpi5-examples
```

```bash
source setup_env.sh
```

Das GitHub-Repository **Hailo-rpi5-examples** bietet verschiedene Beispiele zur Nutzung des Hailo AI Kits mit dem Raspberry Pi 5. Die Funktion der Objekterkennung wird hier jedoch nicht bereitgestellt. Weitere Informationen finden sich auf folgender [Seite](https://github.com/hailo-ai/hailo-rpi5-examples/tree/main).


Um unsere HEF Datei nutzen zu können, müssen folgende Dokumente im hailo_rpi5_examples  in den folgenden Verzechnissen angepasst werden: 

**Ressources Ordner:**

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/ressources.jpeg?raw=true" width="500">

Im **resources**-Ordner werden die JSON-Datei und die HEF-Datei abgelegt. Die JSON-Datei definiert zentrale Parameter für die Modellausführung, zur Orientierung kann die im Ordener bereits hinterlegte **barcode-json** genutzt werden, basierend darauf habe ich für mein Modell folgende json zusammengestellt:

```json
{
    "iou_threshold": 0.4,
    "detection_threshold": 0.5,
    "output_activation": 0.5,
    "label_offset": 0.5,
    "max_boxes":3,
    "labels": [
      "unlabeled",
      "Bauklotz"
    ]
}
```
- Der Parameter **iou_threshold (0.4)** legt fest, dass Bounding Boxen mit mehr als 40 % Überlappung zusammengeführt werden.

- **detection_threshold (0.5)** bedeutet, dass Objekte nur erkannt werden, wenn die Konfidenz mindestens 50 % beträgt.

- Mit **max_boxes (3)** wird die maximale Anzahl der anzuzeigenden Objekte auf drei begrenzt. Die labels enthalten die Klassennamen „unlabeled“ und „Bauklotz“.

Basic-pipeline - Ordner:



<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/pipeline.jpeg?raw=true" width="400">

Im **basic_pipeline**-Ordner wird das Skript Bauklotz_detection.py hinterlegt, das für die Modellausführung angepasst wurde. Dieses Skript ruft die Modellausgabe ab, zeichnet Bounding Boxen um erkannte Objekte und zeigt relevante Informationen wie Klasse, Konfidenz und Verarbeitungsgeschwindigkeit an. Die Skripte detection_pipeline.py und detection.py sind standardmäßig im Repository enthalten, können jedoch an spezifische Anforderungen angepasst werden. Das Skript, das ich verwendet habe, lautet wie folgt:



```python
import gi
gi.require_version('Gst', '1.0')
from gi.repository import Gst, GLib
import os
import numpy as np
import cv2
import hailo
from hailo_rpi_common import (
    get_caps_from_pad,
    get_numpy_from_buffer,
    app_callback_class,
)
from detection_pipeline import GStreamerDetectionApp
import time

# User-defined class for the callback function
class user_app_callback_class(app_callback_class):
    def __init__(self):
        super().__init__()
        self.new_variable = 42

    def new_function(self):
        return "The meaning of life is: "

# Callback function for the pipeline
def app_callback(pad, info, user_data):
    buffer = info.get_buffer()
    if buffer is None:
        return Gst.PadProbeReturn.OK

    user_data.increment()
    string_to_print = f"Frame count: {user_data.get_count()}\n"

    # Get camera resolution
    format, width, height = get_caps_from_pad(pad)
    print(f"Camera Resolution: {width}x{height}")

    frame = None
    if user_data.use_frame and format is not None:
        frame = get_numpy_from_buffer(buffer, format, width, height)
        frame = cv2.resize(frame, (640, 640))  # Resize for display

    roi = hailo.get_roi_from_buffer(buffer)
    detections = roi.get_objects_typed(hailo.HAILO_DETECTION)

    detection_count = 0

    # Start timing
    start_time = time.time()

    for detection in detections:
        label = detection.get_label()
        bbox = detection.get_bbox()
        confidence = detection.get_confidence()

        # Convert normalized to absolute coordinates
        xmin = int(bbox.xmin() * width)
        ymin = int(bbox.ymin() * height)
        xmax = int(bbox.xmax() * width)
        ymax = int(bbox.ymax() * height)

        # Update the shell output to match (xmin, ymin, xmax, ymax)
        string_to_print += f"Detection: {label}, Confidence: {confidence:.2f}, BBox: ({xmin}, {ymin}, {xmax}, {ymax})\n"

        # Draw bounding box and class+confidence as percentage on the frame
        if user_data.use_frame and frame is not None:
            cv2.rectangle(frame, (xmin, ymin), (xmax, ymax), (0, 255, 0), 2)
            # Display label, confidence, and bounding box format
            cv2.putText(frame, f"{label} {int(confidence * 100)}%", (xmin, ymin - 10),
                        cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 255, 0), 2)

        detection_count += 1

    # Measure timing for detection pipeline
    elapsed_time = (time.time() - start_time) * 1000  # Convert to milliseconds

    string_to_print += f"Speed: {elapsed_time:.2f}ms per frame\n"
    print(string_to_print)

    if user_data.use_frame and frame is not None:
        # Display the number of detections
        cv2.putText(frame, f"Detections: {detection_count}", (10, 30),
                    cv2.FONT_HERSHEY_SIMPLEX, 1, (0, 255, 0), 2)
        user_data.set_frame(frame)

    return Gst.PadProbeReturn.OK

if __name__ == "__main__":
    user_data = user_app_callback_class()
    app = GStreamerDetectionApp(app_callback, user_data)
    app.run()
```


### Ausführen der Ausgabe:

Zum Starten der Modellausführung wird folgender Befehl verwendet.

```bash
python basic_pipelines/bauklotz-detection.py --labels-json resources/bauklotz-labels.json --hef resources/yolov8s-hailo8l-barcode.hef --input -rpi
```

Mit --input rpi verweisen wir auf die angecshlossene Raspberry Pi Camera Module 3 Kamera, um zu erfahren, welche anderen Möglichkeiten und Ausgaben wir erhalten können, mit dem detection.py Skript kann folgender Befehl ausgefürt werden:

```bash
python basic_pipelines/detection.py --help
```

Das folgende Bild zeigt die Ausgabe. Die Objekte wurden erfolgreich erkannt und mit Bounding Boxen, Klassennamen sowie Konfidenzwerten versehen.

![image](https://github.com/user-attachments/assets/6c91a661-7dde-479a-90b4-65f2520f9534)

---

## 🌟 Warum wurde eine GitHub Seite erstellt?

Die GitHub-Seite wurde erstellt, um den Code, die Konfigurationen und die Dokumentationen des Projekts zentral zu verwalten und zugänglich zu machen. Während der Arbeit an diesem Projekt haben andere GitHub-Seiten wertvolle Unterstützung geboten, um komplexe Schritte besser zu verstehen und umzusetzen. Aus diesem Grund habe ich beschlossen, für die Bachelorarbeit ebenfalls eine GitHub-Seite zu erstellen, um die Projektschritte übersichtlich zu dokumentieren und mit Nachfolgenden zu teilen. Zudem ist diese Seite eine der ersten deutschen Ressourcen, die sich detailliert mit diesem Thema auseinandersetzt.

---

## 📖 Weitere Links, Quellen und Ressourcen, die genutzt wurden

- [YOLO Dokumentation](https://github.com/ultralytics/yolov5)
- [Roboflow Plattform](https://roboflow.com/)
- [Hailo Developer Resources](https://developer.hailo.ai/)


