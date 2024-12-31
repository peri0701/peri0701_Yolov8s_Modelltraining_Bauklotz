![Banner](https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20%26%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Banner_GitHub%20(2).png)
[![Öffnen in Colab](https://img.shields.io/badge/Open%20in%20Colab-grey?style=flat-square&logo=google-colab&logoColor=F9AB00&labelColor=grey&color=F9AB00)](https://colab.research.google.com/drive/1HF5Xfw9nkeZR3tsj--SE_Bm7zlQYZkEw?usp=sharing)


Willkommen auf der Github Seite zu meiner **Bachelorarbeit**:  
**Entwicklung einer KI-basierten Objekterkennungsapplikation für einen Industrieroboter**.  

---

## 🎯 Übersicht

Im Rahmen meiner Bachelorarbeit habe ich ein Yolov8s Modell für die Objekterkennung eines Bauklotzes entwickelt für den Raspberry Pi 5, dem Raspberry PI AI Kit und der Raspberry PI Camera Module 3 Kamera.  

Diese GitHub-Seite bietet:
- **Zugriff auf wichtige Dokumente, Codes und Ergebnisse**, um die Arbeit für Leser und Mitwirkende nachvollziehbar zu machen.
- **Verlinkungen zu detaillierten Repositories** für spezifische Themenbereiche.

---

## 📂 Projektphasen
1. Erstellung eines benutzerdefinierten Datensatzes mit Roboflow
2. Modelltraining
3. Modellausführung auf dem Raspberry PI 5
---

## 📸 Erstellung eines benutzerdefinierten Datensatzes mit Roboflow
[Roboflow](https://roboflow.com/) erleichtert die Datensatzerstellung durch intuitive Verwaltung, Augmentationsoptionen und den Export in verschiedene Formate. 
Für Projekte, die auf vorhandene Daten angewiesen sind, bietet [Roboflow Universe](https://universe.roboflow.com/) mit über 110.000 offenen Datensätzen eine schnelle und vielseitige Alternative. Von annotierten Rissen in Beton bis hin zu Pflanzenbildern mit Krankheitsmarkierungen bietet die Plattform eine breite Auswahl und spart wertvolle Zeit.

Im Folgenden wird Schritt für Schritt erläutert, wie ein benutzerdefinierter Datensatz in Roboflow erstellt und angepasst werden kann:

### Schritt 1: Projekt erstellen:
Um ein neues Projekt zu erstellen, ist zunächst die [Einrichtung eines Roboflow-Kontos](https://app.roboflow.com/login) erforderlich. Nach der Benennung des Workspaces kann im Roboflow-Dashboard ein Projekt angelegt werden.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(10).gif?raw=true" alt="Demo" width="600">

### Schritt 2: Bilder hochladen:
Im nächsten Schritt können die Daten in das neu erstellte Projekt hochgeladen werden. 
Beim Hochladen eines bereits annotierten Datensatzes erkennt das Dashboard automatisch die Bilder und zugehörigen Annotationen:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(6).gif?raw=true" alt="Demo" width="600">


### Schritt 3: Labeln & Annotation:

- **Manuelles Annotieren:**
Bilder können manuell annotiert werden, indem Objekte im Bild markiert und mit passenden Labels versehen werden. Diese Methode bietet volle Kontrolle über die Präzision der Annotationen, erfordert jedoch mehr Zeit und Aufwand.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(3).gif?raw=true" alt="Demo" width="600">

- **Auto-Labeling:**
Als Alternative zum manuellen Annotieren bietet Roboflow eine Auto-Labeling-Funktion, die den Annotierungsprozess erheblich beschleunigen kann. Hierbei werden Annotationen automatisch erstellt, indem Objekte im Bild beschrieben werden. Die automatisch gelabelten Bilder werden zur Review bereitgestellt, wo sie genehmigt oder abgelehnt werden können, um weitere Anpassungen vorzunehmen.
Hinweis: Die Auto-Labeling-Funktion befindet sich derzeit in der Beta-Version und wird kontinuierlich weiterentwickelt.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(9).gif?raw=true" alt="Demo" width="600">

### Schritt 4: Neue Datensatzversion erstellen
Nachdem Bilder und Annotationen hinzugefügt wurden, kann eine neue Version des Datensatzes generiert werden. Dabei besteht die Möglichkeit, den Datensatz zu skalieren (empfohlen: 640x640 für die spätere Yolov8s Modellnutzung) sowie optional Vorverarbeitungs- und Augmentationsmethoden hinzuzufügen, um die Vielfalt und Robustheit zu erhöhen. Diese Anpassungen können die Modellleistung verbessern, sind jedoch nicht zwingend erforderlich.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(5).gif?raw=true" alt="Demo" width="600">

### Schritt 5: Datensatz exportieren
Sobald eine Datensatzversion generiert wurde, steht der Datensatz zum Export bereit. Dieser kann in verschiedenen Formaten heruntergeladen werden, beispielsweise im Format für YOLOv8. Neben dem Herunterladen des Datensatzes auf den Rechner, kann auch ein Befehl generiert  werden, der für das Training in einem Notebook oder einer anderen Umgebung genutzt werden kann. Der Datensatz sollte auf dem Rechner heruntergeladen werden, da er später bei der HEF konvertierung eine Rolle spielen wird.

Im Beispiel wird gezeigt wie von Roboflow Universe, mein finaler Datensatz zu finden ist und heruntergeladen werden kann. Hier zum Datensatz [Direktlink](https://www.google.com/url?q=https%3A%2F%2Funiverse.roboflow.com%2Fbauklotz%2Fbauklotz-c8zsq%2Fdataset%2F1). die weiteren Schritte sind im nächsten Abschnitt zum Modelltraining auf Google Colab zu finden, in dem ich empfehle das Modelltraining zu absolvieren.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(11).gif?raw=true" alt="Demo" width="600">

✔ Nach dem Export eines Datensatzes kann es sinnvoll sein, ein neues Projekt zu erstellen und den fertigen Datensatz erneut zu importieren. Dadurch können die vom System gesetzten Annotationen der durch Augmentation ergänzten Bilder überprüft und bei Bedarf aus dem Datensatz entfernt werden, falls Proportionen oder andere signifikante Änderungen zu Fehlern in der Objekterkennung führen könnten.

---

## 2. **Modelltraining**
Das Modelltraining wird in [Google Colab](https://colab.research.google.com/drive/1HF5Xfw9nkeZR3tsj--SE_Bm7zlQYZkEw?usp=sharing) durchgeführt, um die Datei best.pt zu generieren. Diese Datei enthält die optimierte Version des trainierten Modells und wird im nächsten Schritt für die Modellausführung auf dem Raspberry Pi 5 benötigt. [![Öffnen in Colab](https://img.shields.io/badge/Open%20in%20Colab-grey?style=flat-square&logo=google-colab&logoColor=F9AB00&labelColor=grey&color=F9AB00)](https://colab.research.google.com/drive/1HF5Xfw9nkeZR3tsj--SE_Bm7zlQYZkEw?usp=sharing) 

---

### 3. **Modellausführung auf dem Raspberry PI 5**
Nach dem Erhalt der best.pt Datei, kann diese über Google Drive auf dem Raspberry Pi 5 heruntergeladen werden.

Für die Nutzung müss zunächst eine virtuelle Umgebung aufgesetzt werden. Diese ermöglichen es, Projekte in isolierten virtuellen Räumen auszuführen, ohne das restliche Betriebssystem oder andere installierte Pakete zu beeinträchtigen. Dadurch können Änderungen und Experimente sicher durchgeführt werden, ohne Risiken für die Stabilität des Systems.

Mit diesem Befehl wird eine neue virtuelle Umgebung mit dem Namen yolo_object erstellt. Die Option --system-site-packages sorgt dafür, dass die virtuelle Umgebung Zugriff auf die global installierten Python-Pakete erhält.
```bash
python3 -m venv --system-site-packages yolo_object 
```

Dieser Befehl aktiviert die zuvor erstellte virtuelle Umgebung yolo_object. Nach der Aktivierung laufen alle Python-Befehle und -Installationen innerhalb dieser isolierten Umgebung, um das Hauptsystem zu schütze
```bash
source yolo_object/bin/activate
```

Das System wird zunächst aktualisiert, um sicherzustellen, dass die neuesten Paketlisten geladen sind und zukünftige Installationen reibungslos verlaufen. Danach wird ein wichtiger Paketmanager für Python installiert, der die Verwaltung von Bibliotheken und Abhängigkeiten erleichtert. Schließlich wird dieser Paketmanager auf die neueste Version aktualisiert, um die Kompatibilität mit modernen Python-Bibliotheken sicherzustellen.
```bash
sudo apt update
sudo apt install python3-pip -y
pip install -U pip
```

Dieser Befehl installiert die YOLOv8-Bibliothek ultralytics zusammen mit allen für den Export notwendigen zusätzlichen Paketen. Damit wird die Objekterkennung mit YOLO auf dem Raspberry Pi ermöglicht.
```bash
pip install ultralytics[export]
```

Ein Neustart des Systems stellt sicher, dass alle Änderungen, wie die Installation von Paketen und Systemaktualisierungen, korrekt übernommen werden.
```bash
sudo reboot
```
### Nutzung von Thonny
Thonny ist eine benutzerfreundliche Entwicklungsumgebung für Python, die sich ideal für Projekte wie die Objekterkennung mit YOLO auf dem Raspberry Pi eignet. Sie unterstützt die Arbeit in virtuellen Umgebungen (venv), wodurch Skripte sicher getestet und ausgeführt werden können, ohne das Hauptsystem des Raspberry Pi zu beeinträchtigen, und erleichtert so die Entwicklung direkt auf der Plattform.
 Innerhalb von Thonny kann man dann die entsprechende virtuelle Umgebung auswählen, wodurch alle Skripte und Pakete, die in diesem Projekt verwendet werden, in der isolierten Umgebung bleiben: Hier ein Video, wie die Verknüpfung von Thony mit der venv erfolgen sollte:

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20%26%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(12).gif?raw=true" alt="Demo" width="600">

Der Ordner der virtuellen Umgebung (venv) befindet sich standardmäßig im aktuellen Arbeitsverzeichnis, in dem der Befehl zur Erstellung ausgeführt wurde. Auf dem Raspberry Pi liegt dieses Verzeichnis meist im Home-Verzeichnis des Benutzers, beispielsweise in /home/pi/. Wird die virtuelle Umgebung mit dem Namen yolo_object erstellt, befindet sich diese anschließend als Unterordner im Home-Verzeichnis unter /home/pi/yolo_object, sofern kein anderes Verzeichnis angegeben wurde. Hier ist das Skript, das in die Benutzeroberfläche eingefügt werden sollte, für das Ausführen des Modells, das vorher in den Ordner der venv gespeichert werden sollte:

```python
import cv2
from picamera2 import Picamera2
from ultralytics import YOLO

# Set up the camera with Picam
picam2 = Picamera2()
picam2.preview_configuration.main.size = (1280, 1280)
picam2.preview_configuration.main.format = "RGB888"
picam2.preview_configuration.align()
picam2.configure("preview")
picam2.start()

# Load YOLOv8
model = YOLO("yolov8n.pt")

while True:
    # Capture a frame from the camera
    frame = picam2.capture_array()
    
    # Run YOLO model on the captured frame and store the results
    results = model(frame)
    
    # Output the visual detection data, we will draw this on our camera preview window
    annotated_frame = results[0].plot()
    
    # Get inference time
    inference_time = results[0].speed['inference']
    fps = 1000 / inference_time  # Convert to milliseconds
    text = f'FPS: {fps:.1f}'

    # Define font and position
    font = cv2.FONT_HERSHEY_SIMPLEX
    text_size = cv2.getTextSize(text, font, 1, 2)[0]
    text_x = annotated_frame.shape[1] - text_size[0] - 10  # 10 pixels from the right
    text_y = text_size[1] + 10  # 10 pixels from the top

    # Draw the text on the annotated frame
    cv2.putText(annotated_frame, text, (text_x, text_y), font, 1, (255, 255, 255), 2, cv2.LINE_AA)

    # Display the resulting frame
    cv2.imshow("Camera", annotated_frame)

    # Exit the program if q is pressed
    if cv2.waitKey(1) == ord("q"):
        break

# Close all windows
cv2.destroyAllWindows()
```
Hier ein Beipiel von der Ausgabe meines Modells:





---

### 4. **Modellkonvertierung in ONNX**
Die Hailo SDK und der Hailo Data Compiler, die später für die Konvertierung des ONNX-Modells in das Hailo Execution Format (HEF) verwendet werden, unterstützen nur ONNX-Modelle bis zu einer bestimmten Opset-Version, die Versionen die ich genutzt habe besitzen eine Obergrenze bei Opset 9. Die Opset-Version definiert die Funktionen und Operatoren, die innerhalb des Modells verwendet werden können. Opset 9 ist eine stabile und weit unterstützte Version, die mit den meisten älteren Frameworks und Tools kompatibel ist, insbesondere mit der HEF-Pipeline.

Die Konvertierung von ONNX kann direkt über eine YOLO CLI von den zuvor heruntergeladenen Ultralytics Paketen durchgeführt werden kann:
```bash
cd env
yolo export model=best.pt imgsz=640 format=onnx opset=9
```
Nach dem Durchführen des Befehls, erhält man folgende Ausgabe und die Information, das die ONNX Datei im selben Ordner, unserer venv, bei mir in "env" gespeichert wurde:

![Bild](https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20%26%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/onnx_conversion.png)

---
### 4. **Modellkonvertierung in HEF**

### 1.Linux-Umfeld herstellen (WSL & Ubuntu 22.04)
Um ein trainiertes Modell auf dem Raspberry Pi AI Kit mit der Hailo-Hardware auszuführen, ist eine Konvertierung des Modells in das Hailo Execution Format (HEF) notwendig. Da die Hailo-Software derzeit ausschließlich auf x86-Linux-Systemen unterstützt wird, bietet die Nutzung von WSL (Windows Subsystem for Linux) eine einfache Lösung für Windows-Nutzer. 

Die Ubuntu 22.04-Version wird zusätzlich über den Microsoft Store heruntergeladen, um eine separate Linux-Applikation bereitzustellen. Obwohl dieser Schritt im ursprünglichen Tutorial nicht vorgesehen war, hat sich die Methode als erfolgreich erwiesen und bietet den Vorteil einer isolierten Arbeitsumgebung mit erhöhter Flexibilität – weshalb ich diese Methode ebenfalls empfehlen würde.

Mit WSL kann eine Ubuntu-Umgebung direkt auf Windows eingerichtet werden, wodurch der gesamte Prozess der Modellkonvertierung wie auf einem nativen Linux-System durchgeführt werden kann, dazu muss zunächst die Powershell geöffnet werden:

```powershell
wsl --list --online
```
```powershell
wsl --install -d Ubuntu-22.04
```
Nach diesem Schritt wird gebeten ein Benutzername und Passwort anzugeben. Das Passwort wird bei allen "sudo" Befehlen angefragt im Ubutu Umfeld

```powershell
sudo apt update
```
```powershell
sudo apt upgrade
```
Hier kann bei Bedarf in die Applikation nun gewechselt werden:


Bild

### 2. Hailo Data Compiler herunterladen 

Der Hailo Dataflow Compiler wird benötigt, um ONNX-Modelle in das für die Hailo-Hardware optimierte HEF-Format zu konvertieren. Er passt Modelle an die Hardwarearchitektur an und ermöglicht durch Optimierungen wie Quantisierung eine maximale Leistung bei minimalem Ressourcenverbrauch.

NUn werden erforderliche Python Pakete heruntergeladen, die wir für den Hailo Data Compiler benötigen.

```powershell
sudo apt install python3-pip
sudo apt install python3.10-venv
sudo apt-get install python3.10-dev python3.10-distutils python3-tk libfuse2 graphviz libgraphviz-dev
sudo pip install pygraphviz
sudo apt install wslu
```
Eine venv aufgestellt:

```powershell
python3 -m venv hailodfc
. hailodfc/bin/activate
```

Um die Kompalität mizt der python Umgebung u sehen - Sie sollte 3.10.12 sein.
```powershell
python3 --version
```

Um den Hailo Dataflower Compiler herunterzuladen muss erst eine Registrierung in die Hailo Developer Zone erfolgen, die [hierüber](https://hailo.ai/authorization/?redirect_to=https%3A%2F%2Fhailo.ai%2Fdeveloper-zone%2Fsoftware-downloads%2F) durchgeführt werden kann. Als nächstes muss die 3.28 Version mit der Python Version 3.10, die am 1.Juli 2024 erschienen ist heruntergeladen werden.

video

Nun muss die heruntergelade Datei in unser Ubuntu "home" Verzeichnis gebracht und abgelegt werden, damit sie in unserem Ubuntu Umfeld auch installiert werden kann, mit folgendem Befehl, öffnet sich das Zielverzeichnis, die Datei muss bon den Downloads in diesen Bereich verschoben werden:

```powershell
wslview .
```

Ist dies erledigt, kann mit dem Befehl, wird die Installation gestartet: 
```powershell
pip3 install hailo_dataflow_compiler-3.28.0-py3-none-linux_x86_64.whl
```

Mt den Befehlen, kann verifiziert werden, ob der Download erfolgreich war, indem man "help" anzeigen lässt:

```powershell
hailo -h
```
 bild

### 3. Hailo Model Zoo herunterladen

In einem nächsten Schritt wird Hailo Modek Zoo heruntergeladen, dazu nutzen wir Hailo AIs Github repository:

```powershell
git clone https://github.com/hailo-ai/hailo_model_zoo.git
```

Und installieren alle darin enthaltenen Pakete die zum Setup dazu gehören:

```powershell
cd hailo_model_zoo; pip install -e .
```

## 4. Vorbereitung auf die HEF Konverterierung 

Nun muss wie vorher die heruntergeladene Hailo Datafllow Compiler auch unsere zuvor enerierte best.onnx Datei in das Ubuntu Verzeichnis gezogen werden - Vom Raspberry Pi kann diese über Google Drive auf dem Rechner heruntergeladen werden.

bild

Beim Herunterladen des Datensatzes wurdn die Bilder und Annotationen in drei Ordner Strukturen aufgeteilt, der train Ordner, muss ebenfalls in das Ubuntu Umfeld gepackt werden.

bild

Viele machen den Fehler den Befehl zur Performance Steigerung jetzt schon auszugeben, da man davon ausgehen kann, dass man alle Komponenten besitzt:


```powershell
hailomz compile yolov8s --ckpt=best.onnx --hw-arch hailo8l --calib-path train/images --classes 1 --performance
```
Im Hintergrund müssen im hailo model zoo, folgende Skripte angepasst werden, die unter folgendem Verzeichnis zu finden sind im Ubuntu Verzeichnis:

#
```json
{
	"nms_scores_th": 0.2,
	"nms_iou_th": 0.7,
	"image_dims": [
		640,
		640
	],
	"max_proposals_per_class": 100,
	"classes": 80,
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


```plaintext
normalization1 = normalization([0.0, 0.0, 0.0], [255.0, 255.0, 255.0])
change_output_activation(conv42, sigmoid)
change_output_activation(conv53, sigmoid)
change_output_activation(conv63, sigmoid)
nms_postprocess("../../postprocess_config/yolov8s_nms_config.json", meta_arch=yolov8, engine=cpu)
```


#



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
  - models_files/ObjectDetection/Detection-COCO/yolo/yolov8s/2023-02-02/yolov8s.onnx
  alls_script: yolov8s.alls
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
  output_shape: 80x5x100
  operations: 28.6G
  parameters: 11.2M
  framework: pytorch
  training_data: coco train2017
  validation_data: coco val2017
  eval_metric: mAP
  full_precision_result: 44.75
  source: https://github.com/ultralytics/ultralytics
  license_url: https://github.com/ultralytics/ultralytics/blob/main/LICENSE
  license_name: GPL-3.0
```

- **Repository-Link**: [Raspberry Pi Deployment](https://github.com/YourUsername/RaspberryPi-Deployment)
- **Inhalt**:
  - Einrichtung der Hardware- und Softwareumgebung.
  - Integration der Kameramodule für die Objekterkennung.
  - Performance-Analyse und Praxistests.




---
### 3. **Modellausführung auf dem Raspberry PI 5**
- **Repository-Link**: [Model Conversion for Hailo](https://github.com/YourUsername/Model-Conversion)
- **Inhalt**:
  - Konvertierung von PyTorch-Modellen zu ONNX.
  - Anpassung an das Hailo Execution Format (HEF).
  - Umgang mit Kompatibilitätsproblemen und Lösungen.
    
---

## 📖 Zusätzliche Dokumentation

Detaillierte Anleitungen und Hintergründe zu den einzelnen Schritten:
- [Einleitung und Motivation](https://your-github-pages-link.com/introduction)
- [Theoretische Grundlagen](https://your-github-pages-link.com/fundamentals)
- [Tutorials für jede Phase](https://your-github-pages-link.com/tutorials)
- [Herausforderungen und Lösungsansätze](https://your-github-pages-link.com/challenges)

---

## 🌟 Warum dieses Projekt?

Dieses Projekt zeigt, wie leistungsstarke, kosteneffiziente Hardware wie der Raspberry Pi in Kombination mit modernen KI-Modellen genutzt werden kann, um industrielle Anwendungen zu verbessern. Es soll anderen Entwicklern und Forschern als Inspiration und Anleitung dienen.

---

## 📬 Kontakt

Für Rückfragen oder Anregungen stehe ich gerne zur Verfügung:
- **E-Mail**: yourname@example.com
- **LinkedIn**: [Dein LinkedIn-Profil](https://linkedin.com/in/yourprofile)

---

## 📎 Weitere Links und Ressourcen

- [YOLO Dokumentation](https://github.com/ultralytics/yolov5)
- [Roboflow Plattform](https://roboflow.com/)
- [Hailo Developer Resources](https://developer.hailo.ai/)


