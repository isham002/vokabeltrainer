# 📱 Vokabeltrainer App (Flutter & Firebase)

Ein plattformübergreifender Vokabeltrainer, der gezielt auf **Microlearning** (Lernen in kurzen Intervallen) und **Gamification** (Streaks, XP und eine Liga-Bestenliste) setzt. Entwickelt als Teamprojekt für das Modul *"Mobile Applikationen"* an der FH Südwestfalen.

---

## 👥 Das Team

Die Anwendung wurde gemeinschaftlich konzipiert und umgesetzt. Die Hauptverantwortlichkeiten im Code waren wie folgt aufgeteilt:
* **Carlo Iuliano ([@Carlo2903](https://github.com/Carlo2903))** – Core-Architektur, Smart Suggest & Kurs-Einstellungen (Haupt-Repository)
* **Melih Acar** – Authentifizierung, Passwort-Reset, Splash Screen & UI-Design
* **Ismail Hamoud** – Kamera-OCR, Offline-Übersetzung & Gamification-Backend

> 💡 **Hinweis zum Fork:** Das Projekt wurde aktiv in Carlos Repository entwickelt: [**Zum Original-Repository**](https://github.com/Carlo2903/vokabeltrainer). Dies hier ist mein persönlicher Mirror, um meine Beiträge für mein Portfolio festzuhalten.

---

## 📸 Screenshots

<p align="center">
  <img width="250" alt="Liga_Bestenliste" src="https://github.com/user-attachments/assets/d2a3aab7-ce2b-43c1-af0b-eaa042c65772" />
  &nbsp;&nbsp;&nbsp;
  <img width="250" alt="Text_aus_Bild_scannen" src="https://github.com/user-attachments/assets/4a1fa1a5-2c83-4e3f-ad2c-4a4af921b57f" />
  &nbsp;&nbsp;&nbsp;
  <img width="250" alt="Training_starten" src="https://github.com/user-attachments/assets/8937a410-0bfb-453e-9609-0ab7d87751b5" />
</p>

---

## 🚀 Meine Schwerpunkte im Code

Mein Fokus lag auf der Implementierung der daten- und logikgetriebenen Kernfeatures der App:

* **Kamera-Import & Offline-Übersetzung:** Integration von *Google ML Kit Text Recognition*. Nutzer können Vokabellisten abfotografieren, woraufhin der Text per OCR erkannt und direkt **offline auf dem Gerät** übersetzt und importiert wird.
* **Gamification-Engine:** Entwicklung des Backend-Fundaments für das Fortschrittssystem (reaktive XP-Berechnung, tägliche Lern-Streaks und Meilenstein-Logik für die Bestenliste).
* **UI-Polishing & Bugfixing:** Behebung kritischer Layout-Fehler (wie z. B. Render-Overflows im `AddVocabularyScreen`) und Optimierung der Navigation (Zurück-Button-Verhalten im Erfolge-Screen).

### 🛠️ Technische "Lessons Learned"
* **R8 / Proguard Fehler gelöst:** Beim Erstellen der Release-APK kam es durch das ML Kit zu Minifizierungs-Konflikten. Gelöst durch die gezielte Konfiguration der Keep-Rules in der `proguard-rules.pro`.
* **Asynchrones State-Management:** Einbindung von Streams aus *Cloud Firestore* in Kombination mit dem *Provider Pattern*, um XP-Updates und die globale Bestenliste flüssig und in Echtzeit zu rendern.

---

## 🛠 Tech-Stack

* **Frontend:** Flutter, Dart
* **State Management:** Provider Pattern (`ChangeNotifier`)
* **Backend & DB:** Firebase Auth, Cloud Firestore (NoSQL)
* **Machine Learning:** Google ML Kit (Text Recognition & Offline Translation)

---

## ⚙️ Lokales Setup

1. **Repository klonen & Verzeichnis wechseln:**
   ```bash
   git clone https://github.com/isham002/vokabeltrainer.git
   cd vokabeltrainer
   ```

2. **Abhängigkeiten installieren:**
   ```bash
   flutter pub get
   ```

3. **Firebase Konfiguration:**
   Da dies ein Firebase-Projekt ist, müssen die eigenen Konfigurationsdateien eingefügt werden:
   * **Android:** `android/app/google-services.json`
   * **iOS:** `ios/Runner/GoogleService-Info.plist`

4. **App starten:**
   ```bash
   flutter run
   ```
