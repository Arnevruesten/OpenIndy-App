benötigte Installationen:
http://ionicframework.com/getting-started/
- Node.js (windows installer)
- Cordova + ionic command line tools (https://www.npmjs.com/package/ionic)
	- Installation via cmd npm
- Installation Cordova + Android SDK (http://learn.ionicframework.com/videos/windows-android/)


Architektur:

Projekt anlegen
- cd zu workspace
- ionic start <name>

Android hinzufügen
- cd in Projektordner
- ionic platform add android

Emulator einrichten
- Android SDK Tools -> AVD Manager
- AVD hinzufügen für jeweiliges ANDroid Version (http://stackoverflow.com/questions/10641744/samsung-galaxy-s-ii-avd-android-virtual-device-basic-settings)

Live Ausführung auf Handy:
- Samsung Kies auf PC installieren
- am Handy bei Entwickleroptionen USB Debugging einschalten
- ionic run android führt dann statt emulator das handy aus



deployment:
- console plugin entfernen: cordova plugin rm org.apache.cordova.console
- build: cordova build --release android
- Generierung eines key-files:
	- im bin Ordner des installierten JDK:
	- keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
- Verschlüsselung des APK:
	- jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore HelloWorld-release-unsigned.apk alias_name
- Alignment Optimierung:
	- unter Android SDK build-tools
	- zipalign -v 4 HelloWorld-release-unsigned.apk HelloWorld.apk
	
Installation:
- Android:
	- unter Einstellungen - Sicherheit - Unbekannte Quellen anhaken
	- Android an PC anschließen und im Explorer öffnen
	- das gebuildete APK in einen Ordner kopieren (z.B. Download)
	- das APK auf dem Smartphone suchen und installieren