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
Sobald eine Datensatzversion generiert wurde, steht der Datensatz zum Export bereit. Dieser kann in verschiedenen Formaten heruntergeladen werden, beispielsweise im Format für YOLOv8, das für das Training in einem Notebook oder einer anderen Umgebung genutzt werden kann. Im Beispiel wird gezeigt wie von Roboflow Universe, mein finaler Datensatz zu finden ist und heruntergeladen werden kann. Hier zum Datensatz [Direktlink](https://www.google.com/url?q=https%3A%2F%2Funiverse.roboflow.com%2Fbauklotz%2Fbauklotz-c8zsq%2Fdataset%2F1). die weiteren Schritte sind im nächsten Abschnitt zum Modelltraining auf Google Colab zu finden, in dem ich empfehle das Modelltraining zu absolvieren.

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
reboot
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
Die Konnvertrierung in ONNX brauchen wir für die spätere Konvertierung in HEF.

Diese kann in der zuvor erstellten venv durchgeführt werden, da dies von den zuvor heruntergeladenen Ultralytics Pketen durchgeführt werden kann:


---
### 4. **Modellkonvertierung in HEF**
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


