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

In einem nächsten Schritt wird Hailo Modek Zoo heruntergeladen, dazu nutzen wir Hailo AIs Github repository:

```powershell
git clone https://github.com/hailo-ai/hailo_model_zoo.git
```

Wechseln das Verzeichnis und installieren alle darin enthaltenen Pakete die zum Setup dazu gehören:

```powershell
cd hailo_model_zoo; pip install -e .
```

## 5. Vorbereitung auf die HEF Konverterierung 

Nun muss wie vorher die heruntergeladene Hailo Datafllow Compiler auch unsere zuvor enerierte best.onnx Datei in das Ubuntu Verzeichnis gezogen werden - Vom Raspberry Pi kann diese über Google Drive auf dem Rechner heruntergeladen werden.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/best.jpeg?raw=true"  width="400">

Beim Herunterladen des Datensatzes wurdn die Bilder und Annotationen in drei Ordner Strukturen aufgeteilt, der train Ordner, muss ebenfalls in das Ubuntu Umfeld gepackt werden.


<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/trsin_folder.jpeg?raw=true" width="400">

Viele machen den Fehler den Befehl zur Performance Steigerung jetzt schon auszugeben, da man davon ausgehen kann, dass man alle Komponenten besitzt:


```powershell
hailomz compile yolov8s --ckpt=best.onnx --hw-arch hailo8l --calib-path train/images --classes 1 --performance
```
Im Hintergrund müssen im hailo model zoo, folgende Skripte angepasst werden, die unter folgendem Verzeichnis zu finden sind im Ubuntu Verzeichnis:

# 
![image](https://github.com/user-attachments/assets/4172ebb3-c527-4208-8819-20472d413967)

Gegebenfalls anpassen, mein Model ist auf ein 640x640 Format trainiert worden  # hier die Klassenanzahl angeben, hier 1

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

#
![image](https://github.com/user-attachments/assets/2905ce2d-8423-4528-ace4-11579f15bf11)


```plaintext
quantization_param([conv42, conv53, conv63], force_range_out=[0.0, 1.0])
normalization1 = normalization([0.0, 0.0, 0.0], [255.0, 255.0, 255.0])
change_output_activation(conv42, sigmoid)
change_output_activation(conv53, sigmoid)
change_output_activation(conv63, sigmoid)
performance_param(compiler_optimization_level=max)
nms_postprocess("../../postprocess_config/yolov8s_nms_config.json", meta_arch=yolov8, engine=cpu)
```


#

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/network.jpeg?raw=true" width="400">

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
  alls_script: hailo_model_zoo/hailo_model_zoo/cfg/alls/yolov8s.alls #Hier muss der genaue Pfad zur yolov8s.alls Datei angegeben werden 
  url: https://hailo-model-zoo.s3.eu-west-2.amazonaws.com/ObjectDetection/Detection-COCO/yolo/yolov8s/2023-02-02/yolov8s.zip
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
  output_shape: 1x5x100 #Erste Zahl steht für die Klasse (1=Bauklotz)
  operations: 28.4G #Entspricht GFLOPs der "Model Summary(fused)"   Angabe meines Modeltrainings
  parameters: 11.125M #Entspricht den parametern der "Model Summary(fused)" des Modelltrainings 
  framework: pytorch
  training_data: coco train2017
  validation_data: coco val2017
  eval_metric: mAP
  full_precision_result: 44.75
  source: https://github.com/ultralytics/ultralytics
  license_url: https://github.com/ultralytics/ultralytics/blob/main/LICENSE
  license_name: GPL-3.0
```

Ist die Optimierung abgeschlossen, erhält die Information, dass die Hef datei gespeichert wurde.
![image](https://github.com/user-attachments/assets/7183d63d-2382-4a96-a527-8c46464e1d64)

---
## 6. **Modellausführung auf dem Raspberry PI 5 & Ai KIT**

Dafür muss das entsprechende Umfeld erst geschaffen werden, dafür wird das Hailo rpi5 Examples repository auf dem Raspberry Pi heruntergeladen.

```bash
git clone https://github.com/hailo-ai/hailo-rpi5-examples.git
```
```bash
cd hailo-rpi5-examples
```
```bash
./install.sh
```
Falls der ./install.sh nicht auf anhieb funktionieren sollte, so gibt es eine Zweite Möglichkeit die benötigten Packete herunterzuladen, eine venv wird manuell durch folgenden Link erstellt, hier: 

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

Wenn die venv geschlossen wird und man eine neue Terminal session benutzen möchte mit den Paketen, so sollte immer source setup_env.sh verwendet werden. 

**Hinweis:** Man muss isch im hailo-rpi5-examples Verzeichnis befinden!
Wie folgt ist nach einer neuen Terminal Session vorzugehen:

```bash
cd hailo-rpi5-examples
```

```bash
source setup_env.sh
```

Es gibt im Hailo-rpi5-examples GitHub verschiede Beispiele, wie der Hailo AI Kit mit dem Raspberry Pi5 genutzt werden kann, außer der Object detection Funktion, [hier](https://github.com/hailo-ai/hailo-rpi5-examples/tree/main) ein Link zur Seite.


Um unsere HEF Datei nutzen zu können, müssen folgende Dokumente in den folgenden Verzechnissen hinterlegt werden: 



<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/pipeline.jpeg?raw=true" width="400">

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/ressources.jpeg?raw=true" width="400">

Folgender Befehl wird dann zum Ausführen ausgeführt, input hier ist unsere Raspberry PI 3 Camera Module Kamera:

```bash
python basic_pipelines/bauklotz-detection.py --labels-json resources/bauklotz-labels.json --hef resources/yolov8s-hailo8l-barcode.hef --input -rpi
```

Hier die Ausgabe:

![image](https://github.com/user-attachments/assets/916cb36c-8beb-4041-ba46-8535442ebe21)


---

## 📖 Zusätzliche Dokumentation

Detaillierte Anleitungen und Hintergründe zu den einzelnen Schritten:
- [Einleitung und Motivation](https://your-github-pages-link.com/introduction)
- [Theoretische Grundlagen](https://your-github-pages-link.com/fundamentals)
- [Tutorials für jede Phase](https://your-github-pages-link.com/tutorials)
- [Herausforderungen und Lösungsansätze](https://your-github-pages-link.com/challenges)

---

## 🌟 Warum wurde eine GitHub Seite erstellt?

Dieses Projekt zeigt, wie leistungsstarke, kosteneffiziente Hardware wie der Raspberry Pi in Kombination mit modernen KI-Modellen genutzt werden kann, um industrielle Anwendungen zu verbessern. Es soll anderen Entwicklern und Forschern als Inspiration und Anleitung dienen.

---

## 📎 Weitere Links und Ressourcen

- [YOLO Dokumentation](https://github.com/ultralytics/yolov5)
- [Roboflow Plattform](https://roboflow.com/)
- [Hailo Developer Resources](https://developer.hailo.ai/)


