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

## 📸 Benutzerdefinierte Datensatzerstellug in Roboflow

Roboflow bietet eine effiziente Plattform, die diesen Prozess durch einfache Verwaltung, Augmentationsoptionen und Exportmöglichkeiten in verschiedene Formate erheblich erleichtert. Im Folgenden wird Schritt für Schritt gezeigt, wie man auf Roboflow einen Datensatz erstellt, anpasst und für die weitere Nutzung herunterladen kann:

**Schritt 1: Projekt erstellen:**
Um ein neues Projekt zu erstellen, ist zunächst die Einrichtung eines Roboflow-Kontos erforderlich. Anschließend kann im Roboflow-Dashboard ein Projekt angelegt werden, wobei der passende Projekttyp, wie beispielsweise Objekterkennung, ausgewählt werden sollte:
<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(2).gif?raw=true" alt="Demo" width="600">

**Schritt 2: Bilder hochladen:**
Im nächsten Schritt können die Daten in das neu erstellte Projekt hochgeladen werden. 
Beim Hochladen eines bereits annotierten Datensatzes erkennt das Dashboard automatisch die Bilder und zugehörigen Annotationen.
<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(6).gif?raw=true" alt="Demo" width="600">

**Schritt 3: Labeln:**
Neben der Möglichkeit, Bilder manuell zu annotieren, bietet Roboflow eine Auto-Labeling-Funktion an, die im . Diese ermöglicht es, durch die Beschreibung eines Objekts Annotationen automatisch auf den Bildern zu erstellen. Automatisch gelabelte Bilder werden anschließend zur Review bereitgestellt, wo sie genehmigt oder abgelehnt werden können, um weitere Anpassungen vorzunehmen.

## 📹 Demonstrationsvideo


<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(3).gif?raw=true" alt="Demo" width="600">
<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(4).gif?raw=true).gif?raw=true" alt="Demo" width="600">
<img src="https://github.com/peri0701/Bauklotz-Objekterkennungsmodell/blob/main/Bilder%20&%20Videos%20f%C3%BCr%20die%20GitHub%20Seite/Video3%20(5).gif?raw=true" alt="Demo" width="600">



---

### 2. **Modelltraining**
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


