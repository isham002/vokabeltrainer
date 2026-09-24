# 📱 Vokabeltrainer (Flutter & Firebase)

Ein plattformübergreifender Vokabeltrainer, der gezielt auf Microlearning (Lernen in kurzen Intervallen) und Gamification (Streaks, XP, Liga-Bestenliste) setzt. Die Anwendung ermöglicht flexibles Lernen mit unmittelbarem visuellen Feedback.

Das System wurde als praktische Prüfungsleistung im Modul 'Mobile Applikationen' an der FH Südwestfalen entwickelt. Der Fokus lag auf einer serverlosen Client-Server-Architektur, plattformübergreifender Entwicklung und der Integration von On-Device Machine Learning (OCR).
> 💡 **Portfolio-Hinweis:** Dieses Repository ist mein persönlicher Entwickler-Mirror zur Dokumentation meiner Kernbeiträge. Das gemeinschaftliche Haupt-Projekt liegt im [Original-Repository von Carlo Iuliano](https://github.com/Carlo2903/vokabeltrainer).

---

## 👥 Team & Aufgabenverteilung

Wir haben das Projekt agil aufgeteilt und die Verantwortlichkeiten nach Kernarchitektur und Feature-Sets getrennt:

* **Ismail Hamoud (Mein Bereich):** Implentierung der Core-Features und der Gamification-Engine. Dazu gehören der Kamera-Import via OCR inklusive On-Device Offline-Übersetzung sowie das komplette Gamification-Backend (reaktive XP-Berechnung, tägliche Streaks und die globale Liga-Bestenliste).
* **Carlo Iuliano ([@Carlo2903](https://github.com/Carlo2903)):** Core-Architektur, Smart Suggest System und globale App-Einstellungen.
* **Melih Acar:** Firebase Authentication UI-Design und die automatisierte Passwort-Reset-Pipeline.

---

## 📸 UI & Features

<p align="center">
  <img width="250" alt="Liga_Bestenliste" src="https://github.com/user-attachments/assets/d2a3aab7-ce2b-43c1-af0b-eaa042c65772" />
  &nbsp;&nbsp;&nbsp;
  <img width="250" alt="Text_aus_Bild_scannen" src="https://github.com/user-attachments/assets/4a1fa1a5-2c83-4e3f-ad2c-4a4af921b57f" />
  &nbsp;&nbsp;&nbsp;
  <img width="250" alt="Training_starten" src="https://github.com/user-attachments/assets/8937a410-0bfb-453e-9609-0ab7d87751b5" />
</p>

* **Smarter Import (OCR):** Nutzer können analoge Vokabellisten abfotografieren. Mittels Google ML Kit wird der Text extrahiert und vollständig offline auf dem Endgerät übersetzt.
* **Gamification-Engine:** Ein motivierendes System mit Echtzeit-XP-Berechnung, täglichen Streaks (Lernserien) und einer dynamischen, globalen Liga-Bestenliste.
* **Microlearning-Fokus:** Kurze Lerneinheiten für den Alltag, unterstützt durch *Smart Suggest* und *Auto-fill* beim Eintragen neuer Vokabeln.

---

## 🏗 Architektur & Datenmodell

* **Frontend:** Deklaratives UI-Design mit **Flutter & Dart**. Das State Management wird über das **Provider-Pattern** (`ChangeNotifier`) gelöst, um reaktive UI-Updates zu garantieren.
* **Backend & Auth:** Vollständig serverlose Infrastruktur über **Firebase**. Die Benutzerauthentifizierung erfolgt sicher über Firebase Auth.
* **Datenbank:** **Cloud Firestore** (NoSQL). Das Datenmodell trennt Benutzerdaten strikt über eine Hauptkollektion (`users`) und verschachtelte Sub-Kollektionen (`vocabularies`), um Datensicherheit und schnelle Abfragen zu gewährleisten.

---

## 🧠 Technische Herausforderungen & Lösungen

### 1. Asynchrones State-Management & UI-Blocking
* **Problem:** Die Echtzeit-Synchronisation der Liga-Bestenliste und parallele XP-Updates führten bei hoher Datenlast zu spürbaren Rucklern auf dem UI-Main-Thread.
* **Lösung:** Direkte Kopplung asynchroner Firestore-Streams an das Provider-Pattern. Datenströme werden nun im Hintergrund verarbeitet und UI-Komponenten dank selektiver Repaints flüssig gerendert.

### 2. R8 / ProGuard Code-Minimierungskonflikte
* **Problem:** Beim Generieren der Release-APK schlug der Build-Prozess aufgrund von Code-Optimierungen (Minifizierung) fehl. Die nativen C++ Bibliotheken von Google ML Kit wurden fälschlicherweise obfuscated.
* **Lösung:** Manuelle Konfiguration spezifischer Keep-Rules in der `proguard-rules.pro`, um die ML-Kit-Klassen von der Minifizierung auszuschließen und die Laufzeit-Stabilität zu sichern.

---

## 🛠 Tech-Stack

| Schicht | Technologie |
| :--- | :--- |
| **Frontend-Framework** | Flutter (Dart) |
| **State Management** | Provider Pattern (`ChangeNotifier`) |
| **Datenbank & Auth** | Cloud Firestore, Firebase Authentication |
| **Machine Learning** | Google ML Kit (On-Device OCR & Translation) |

---

## ⚙️ Lokales Setup

### Voraussetzungen
* Installiertes **Flutter SDK**
* Registriertes **Firebase-Projekt**
* Ein eingerichteter Emulator oder ein physisches Testgerät

### Installation & Ausführung

**1. Repository klonen**
```bash
git clone https://github.com/isham002/vokabeltrainer.git
cd vokabeltrainer
```

**2. Abhängigkeiten installieren**
```bash
flutter pub get
```

**3. Firebase-Konfiguration hinterlegen**
Da es sich um ein serverless Projekt handelt, müssen eigene Firebase-Konfigurationsdateien in folgende Pfade hinterlegt werden:
* **Android:** `android/app/google-services.json`
* **iOS:** `ios/Runner/GoogleService-Info.plist`

**4. App starten**
```bash
flutter run
```

*Hinweis zum Testen:* Ein neuer Test-Account kann direkt über den Registrierungsbildschirm der App erstellt werden.

---

## 📄 Lizenz

Dieses Projekt ist unter der **MIT-Lizenz** lizenziert. Weitere Details findest du in der `LICENSE`-Datei.
