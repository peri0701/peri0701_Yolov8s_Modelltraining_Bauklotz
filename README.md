![Banner](https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20%26%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Banner_github.png)


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
1. Benutzerdefinierte Datensatzerstellug in Roboflow
2. 
---

## 📸 Erstellung benutzerdefinierter Datensätze mit Roboflow
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
Sobald eine Datensatzversion generiert wurde, steht der Datensatz zum Export bereit. Dieser kann in verschiedenen Formaten heruntergeladen werden, beispielsweise im Format für YOLOv8, das für das Training in einem Notebook oder einer anderen Umgebung genutzt werden kann. 

**Hinweis**: Im Tutorial wird exemplarisch das Exportieren für YOLOv5 PyTorch gezeigt, was den generellen Prozess veranschaulichen soll. Die Vorgehensweise ist jedoch ähnlich und lässt sich problemlos auf YOLOv8 übertragen.

<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(4).gif?raw=true.gif?raw=true" alt="Demo" width="600">

✔ Nach dem Export eines Datensatzes kann es sinnvoll sein, ein neues Projekt zu erstellen und den fertigen Datensatz erneut zu importieren. Dadurch können die vom System gesetzten Annotationen der durch Augmentation ergänzten Bilder überprüft und bei Bedarf aus dem Datensatz entfernt werden, falls Proportionen oder andere signifikante Änderungen zu Fehlern in der Objekterkennung führen könnten.

---

## 2. **Modelltraining**
- **Repository-Link**: [YOLO Model Training](https://github.com/YourUsername/Model-Training)
- **Inhalt**:
  - Training und Feinabstimmung von YOLO-Modellen.
  - Nutzung von Google Colab für beschleunigtes Training.
  - Optimierung von Trainingsparametern für höhere Genauigkeit.

---

### 3. **Modellausführung auf dem Raspberry PI 5**
- **Repository-Link**: [Model Conversion for Hailo](https://github.com/YourUsername/Model-Conversion)
- **Inhalt**:
  - Konvertierung von PyTorch-Modellen zu ONNX.
  - Anpassung an das Hailo Execution Format (HEF).
  - Umgang mit Kompatibilitätsproblemen und Lösungen.

---

### 4. **Modellkonvertierung in ONNX**
- **Repository-Link**: [Raspberry Pi Deployment](https://github.com/YourUsername/RaspberryPi-Deployment)
- **Inhalt**:
  - Einrichtung der Hardware- und Softwareumgebung.
  - Integration der Kameramodule für die Objekterkennung.
  - Performance-Analyse und Praxistests.

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


