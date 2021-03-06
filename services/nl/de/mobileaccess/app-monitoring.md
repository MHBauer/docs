---

copyright:
  years: 2015, 2016
  
---

# Anwendungen überwachen
{: #app-monitoring}
*Letzte Aktualisierung: 28. Juni 2016*
{: .last-updated}

Neben Sicherheitseinrichtungen stellt {{site.data.keyword.amafull}} auch Überwachungs- und Analysefunktionen für Ihre mobilen Anwendungen bereit. Mit dem {{site.data.keyword.amashort}}-Client-SDK können Sie Clientprotokolle und Überwachungsdaten aufzeichnen. Entwickler können steuern, wann diese Daten an den {{site.data.keyword.amashort}}-Service gesendet werden sollen. Alle Sicherheitsereignisse, wie zum Beispiel erfolgreiche oder fehlgeschlagene Authentifizierungen, die im {{site.data.keyword.amashort}}-Service auftreten, werden automatisch protokolliert.

**Anmerkung**: Die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} sollen auf den neuen Service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics) migriert werden. Das neue Swift-SDK nutzt den neuen Service {{site.data.keyword.mobileanalytics_short}}, der eine deutlich umfangreichere Analyseerfahrung bereitstellt. Der Service {{site.data.keyword.mobileanalytics_short}} befindet sich aktuell in der Versuchsphase und soll planmäßig noch dieses Jahr allgemein verfügbar gemacht werden. Es empfiehlt sich, die Migration Ihrer Anwendungen zum Verwenden des neuen Service {{site.data.keyword.mobileanalytics_short}} und des Swift-SDK zu prüfen, da die Verwendung und Unterstützung der Überwachungsfunktionen des Service {{site.data.keyword.amashort}} eingestellt werden sollen, wenn {{site.data.keyword.mobileanalytics_short}} allgemein verfügbar ist.

Wenn Daten an {{site.data.keyword.amashort}} übergeben werden, können Sie das {{site.data.keyword.amashort}}-Überwachungsdashboard verwenden, um Analyseerkenntnisse zu Ihren mobilen Anwendungen, Geräten und Clientprotokollen zu erhalten. Informationen zu Anforderungen, die Ihre Anwendung an Ressourcen sendet, die von {{site.data.keyword.amashort}} geschützt werden, werden standardmäßig aufgezeichnet.

Zu den automatisch aufgezeichneten Daten gehören Informationen wie die Anzahl der Authentifizierungen, der neuen Geräte und der neuen Benutzer. Darüber hinaus können Sie das {{site.data.keyword.amashort}}-Client-SDK so konfigurieren, dass es die folgenden Informationen zurückmeldet:

### Nutzungsstatistikdaten der mobilen Anwendungen
{: #usage-stats}

Sie können Ihre mobilen Anwendungen so konfigurieren, dass sie mit einigen einfachen API-Aufrufen Anwendungslebenzyklusereignisse aufzeichnen und die aufgezeichneten Daten an den {{site.data.keyword.amashort}}-Service senden. Sie können die Anzahl der Öffnungsvorgänge für Apps, der empfangenen Push-Benachrichtigungen usw. aufzeichnen.

### Clientseitige Protokollerfassung
{: #client-side-logcapture}

Bei Anwendungen in diesem Bereich kommt es ab und zu zu Problemen, die von einem Entwickler behoben werden müssen. Es ist häufig schwer, diese Probleme zu reproduzieren. <!--in R&D.--> Entwickler, die an dem Code gearbeitet haben, verfügen möglicherweise nicht über die Umgebung oder das richtige Gerät, um die entsprechenden Tests durchzuführen. In diesen Situationen ist es hilfreich, die Debugprotokolle von den Clientgeräten abrufen zu können, da die Probleme in der Umgebung auftreten, in der die Ereignisse stattfinden.

### Erfasste Daten beibehalten
{: #preserve-captureddata}

Es gibt keine Möglichkeit sicherzustellen, dass alle erfassten Daten auf der Clientseite erhalten bleiben. Benutzer können die mobile Anwendung offline verwenden und gleichzeitig erfasste Analyse- und Protokolldaten kumulieren. Da der Client offline begrenzten Dateisystemspeicherbereich hat, müssen ältere protokollierte Ereignisse gelöscht werden, um neuere protokollierte Ereignisse behalten zu können. Der Entwickler muss entscheiden, wann erfasste Daten über die bereitgestellten APIs an den {{site.data.keyword.amashort}}-Service gesendet werden sollen.

## {{site.data.keyword.amashort}}-Überwachungsdashboard verwenden
{: #monitoring-dashboard}

1. Öffnen Sie das {{site.data.keyword.Bluemix}}-Dashboard und klicken Sie auf Ihre {{site.data.keyword.Bluemix_notm}}-Anwendung.

2. Wenn Ihr {{site.data.keyword.Bluemix_notm}}-Anwendungsdashboard geöffnet ist, klicken Sie auf eine {{site.data.keyword.amashort}}-Kachel.

3. Klicken Sie im {{site.data.keyword.amashort}}-Dashboard auf den Link **Überwachung** im Menü auf der linken Seite.

## Protokollfunktion aktivieren, konfigurieren und verwenden
{: #enable-logger}

Das {{site.data.keyword.amashort}}-Client-SDK stellt ein Protokollierungsframework bereit, das anderen Protokollierungsframeworks, mit denen Sie vielleicht vertraut sind, wie `java.util.logging` oder `log4j`, ähnlich ist. Das Protokollierungsframework unterstützt mehrere Protokollierungsinstanzen auf Paketbasis, verschiedene Protokollierungsstufen, die Erfassung von Stack-Traces für einen Anwendungsabsturz und weitere Funktionen.

Zudem können Sie die protokollierten Daten zur Speicherung in einem lokalen Speicher konfigurieren, der auf Anforderung an den {{site.data.keyword.amashort}}-Service gesendet werden kann.

Das Protokollierungsframework des {{site.data.keyword.amashort}}-Client-SDK unterstützt die folgenden Protokollierungsstufen, die mit steigender Ausführlichkeit sowie mit Hinweisen zur jeweils empfohlenen Verwendung aufgeführt werden:

* `FATAL` - Wird für nicht behebbare Abstürze oder Blockierungen verwendet. Die Stufe FATAL ist für die Protokollierung nicht behebbarer Fehler reserviert, die für Benutzer wie ein Anwendungsabsturz aussehen.
* `ERROR` - Wird für unerwartete Ausnahmen oder unerwartete Netzprotokollfehler verwendet.
* `WARN` - Dient zur Protokollierung von Warnungen, die nicht als kritische Fehler betrachtet werden (z. B. die Verwendung veralteter APIs oder langsame Netzantwortzeiten).
* `INFO` - Wird zur Meldung von Initialisierungsereignissen und anderen Daten verwendet, die von Nutzen sein können.
* `DEBUG` - Wird zur Meldung von Debuganweisungen verwendet, die Entwicklern bei der Behebung von Anwendungsmängeln helfen.

Stellen Sie sicher, dass Sie das {{site.data.keyword.amashort}}-Client-SDK initialisieren, bevor Sie das Protokollierungsframework verwenden. Die folgenden Beispiel veranschaulichen die grundlegende Verwendung des Protokollierungsframeworks aus dem {{site.data.keyword.amashort}}-Client-SDK.

**Wichtig**: Die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} sollen auf den neuen Service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics) migriert werden. Das neue Swift-SDK nutzt den neuen Service {{site.data.keyword.mobileanalytics_short}}, der eine deutlich umfangreichere Analyseerfahrung bereitstellt. Der Service {{site.data.keyword.mobileanalytics_short}} befindet sich aktuell in der Versuchsphase und soll planmäßig noch dieses Jahr allgemein verfügbar gemacht werden. Es empfiehlt sich, die Migration Ihrer Anwendungen zum Verwenden des neuen Service {{site.data.keyword.mobileanalytics_short}} und des Swift-SDK zu prüfen, da die Verwendung und Unterstützung der Überwachungsfunktionen des Service {{site.data.keyword.amashort}} eingestellt werden sollen, wenn {{site.data.keyword.mobileanalytics_short}} allgemein verfügbar ist.

#### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(context, appRoute, appGUID);

Logger logger = Logger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

#### iOS - Objective-C
{: #enable-logger-objectc}

**Wichtig**: Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix}} Mobile Services, seine Verwendung und Unterstützung sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden.

Das Objective-C-SDK meldet Überwachungsdaten an die Überwachungskonsole des Service {{site.data.keyword.amashort}}. Falls Sie auf die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} angewiesen sind, verwenden Sie weiterhin das Objective-C-SDK.

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

#### iOS - Swift
{: #enable-logger-swift}

```Swift
IMFClient.sharedInstance().initializeWithBackendRoute(appRoute, backendGUID: appGuid)

let logger = IMFLogger(forName: "myLogger");

logger.logDebugWithMessages("debug");
logger.logInfoWithMessages("info");
logger.logWarnWithMessages("warn");
logger.logErrorWithMessages("error");
logger.logFatalWithMessages("fatal");
```

**Anmerkung:** Das {{site.data.keyword.amashort}}-Client-SDK ist mit Objective-C implementiert. Daher müssen Sie Ihrem Swift-Projekt möglicherweise die Datei `IMFLoggerExtension.swift` hinzufügen, um die vorherige Protokollierungs-API verwenden zu können. Sie finden diese Datei im [{{site.data.keyword.amashort}}-Client-SDK-Archiv](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(appRoute , appGUID);

var logger = MFPLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");

```

In den Logger-Klassen sind die folgenden zusätzlichen Methoden zu finden:

* `setCapture` - Dient zum Aktivieren oder Inaktivieren der Speicherung von Protokolldaten, die später an den {{site.data.keyword.amashort}}-Service gesendet werden sollen.
* `setLevel` - Dient zum Festlegen der Protokollierungsstufe für die Speicherung von Protokollnachrichten.
* `send` - Sendet gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service.

Wenn beispielsweise die Erfassung auf ON gesetzt und als Protokollierungsstufe FATAL konfiguriert ist, erfasst die Protokollfunktion nicht abgefangene Ausnahmebedingungen. Nicht abgefangene Ausnahmebedingungen erscheinen Benutzern häufig als Anwendungsabstürze. Es werden jedoch keine Protokolle erfasst, die den Weg zum Absturzereignis aufzeigen. Alternativ stellt eine ausführlichere Protokollierungsstufe sicher, dass Protokolle, die zu dem Protokolleintrag der Stufe FATAL geführt haben, wie zum Beispiel Warnungen (WARN) und Fehler (ERROR), auch erfasst werden.

**Anmerkung:** Vollständige Referenzinformationen zur Logger-API für jede Plattform finden Sie unter [SDKs, Beispiele und API-Referenzen](sdks-samples-apis.html). Die Logger-API gehört zum Kern (Core) des {{site.data.keyword.amashort}}-Client-SDK.


### Verwendungsbeispiel
{: #sample-logger-usage}

Die folgenden Code-Snippets zeigen ein Beispiel für die Verwendung der Protokollfunktion (Logger):

#### Android
{: #enable-logger-sample-android}

```Java
// Speicherung von Protokollen aktivieren
Logger.setCapture(true);

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
Logger.setLevel(Logger.LEVEL.INFO);

// Zwei Logger-Instanzen erstellen
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.debug("debug message");
logger2.info("info message");

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
Logger.send();
```

#### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Speicherung von Protokollen aktivieren
[IMFLogger setCapture:YES];

// Erfassung nicht abgefangener Ausnahmen starten
[IMFLogger captureUncaughtExceptions];

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Zwei Logger-Instanzen erstellen
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Nachrichten mit unterschiedlichen Stufen protokollieren
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
[IMFLogger send];
```

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Speicherung von Protokollen aktivieren
IMFLogger.setCapture(true)

// Erfassung nicht abgefangener Ausnahmen starten
IMFLogger.captureUncaughtExceptions()

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Zwei Logger-Instanzen erstellen
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
IMFLogger.send()

```

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Speicherung von Protokollen aktivieren
MFPLogger.setCapture(true);

// Auszugebende und zu speichernde Mindestprotokollstufe festlegen
MFPLogger.setLevel(MFPLogger.INFO);

// Zwei Logger-Instanzen erstellen
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");    

// Nachrichten mit unterschiedlichen Stufen protokollieren
logger1.debug("debug message");
logger2.info("info message");

// Gespeicherte Protokolle an den {{site.data.keyword.amashort}}-Service senden
MFPLogger.send(success, failure);
```

### Interne Protokolle für das {{site.data.keyword.amashort}}-Client-SDK aktivieren
{: #enable-logger-sdklogs}
Diese Funktion ist gegenwärtig nur in der Android-Version des {{site.data.keyword.amashort}}-Client-SDK verfügbar.

Das {{site.data.keyword.amashort}}-Client-SDK ermöglicht eine bequemere Entwicklungsarbeit, indem es die Logcat-Ausgabe nicht unbedingt durch interne Debugnachrichten erweitert. Daher werden interne Protokollnachrichten, die vom {{site.data.keyword.amashort}}-SDK bei der Stufe DEBUG generiert werden, standardmäßig nicht ausgegeben. Sie können die Ausgabe aller interner Protokollnachrichten des {{site.data.keyword.amashort}}-Client-SDK mit der folgenden API aktivieren:


```
Logger.setSDKInternalLoggingEnabled(true);
```

## Nutzungsanalysedaten erfassen
{: #usage-analytics}

Sie können das {{site.data.keyword.amashort}}-Client-SDK so konfigurieren, dass Nutzungsanalysedaten aufgezeichnet und die aufgezeichneten Daten an den {{site.data.keyword.amashort}}-Service gesendet werden.

**Wichtig**: Die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} sollen auf den neuen Service [{{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics) migriert werden. Das neue Swift-SDK nutzt den neuen Service {{site.data.keyword.mobileanalytics_short}}, der eine deutlich umfangreichere Analyseerfahrung bereitstellt. Der Service {{site.data.keyword.mobileanalytics_short}} befindet sich aktuell in der Versuchsphase und soll planmäßig noch dieses Jahr allgemein verfügbar gemacht werden. Es empfiehlt sich, die Migration Ihrer Anwendungen zum Verwenden des neuen Service {{site.data.keyword.mobileanalytics_short}} und des Swift-SDK zu prüfen, da die Verwendung und Unterstützung der Überwachungsfunktionen des Service {{site.data.keyword.amashort}} eingestellt werden sollen, wenn {{site.data.keyword.mobileanalytics_short}} allgemein verfügbar ist.

**Anmerkung:** Stellen Sie sicher, dass Sie die Protokollerfassung aktiviert haben, bevor Sie die Aufzeichnung von Nutzungsanalysedaten starten.

Verwenden Sie die folgenden APIs, um die Aufzeichnung und das Senden von Nutzungsanalysedaten zu starten:

#### Android
{: #usage-analytics-android}

```Java
// Aufzeichnung von Nutzungsanalysedaten aktivieren
MFPAnalytics.enable();

// Aufzeichnung der Anwendungsstartzeit starten.
// Fügen Sie diesen Code in der Methode 'onCreate' Ihrer Hauptaktivität hinzu.
MFPAnalytics.startLoggingApplicationStartup();

// Dauer des Anwendungsstarts aufzeichnen.
// Fügen Sie diesen Code in der Methode 'onStart' Ihrer Hauptaktivität hinzu.
MFPAnalytics.logApplicationStartup();

// Vorder- und Hintergrundereignisse der Anwendung aufzeichnen.
// Fügen Sie diesen Code in den Methoden 'onPause' und 'onResume' Ihrer Hauptaktivität hinzu.
MFPAnalytics.logSessionStart();
MFPAnalytics.logSessionEnd();

// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
MFPAnalytics.send();
```

#### iOS - Objective-C
{: #usage-analytics-objectc}

**Wichtig**: Das Objective-C-SDK wird zwar weiterhin vollständig unterstützt und gilt noch als primäres SDK für {{site.data.keyword.Bluemix}} Mobile Services, seine Verwendung und Unterstützung sollen jedoch zugunsten des neuen Swift-SDK noch dieses Jahr eingestellt werden.

Das Objective-C-SDK meldet Überwachungsdaten an die Überwachungskonsole des Service {{site.data.keyword.amashort}}. Falls Sie auf die Überwachungsfunktionen des Service {{site.data.keyword.amashort}} angewiesen sind, verwenden Sie weiterhin das Objective-C-SDK.

```Objective-C
// Aufzeichnung von Nutzungsanalysedaten aktivieren
[[IMFAnalytics sharedInstance] setEnabled:YES];

// Aufzeichnung von Anwendungslebenszyklusereignissen starten
[[IMFAnalytics sharedInstance] startRecordingApplicationLifecycleEvents];


// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
[[IMFAnalytics sharedInstance] sendPersistedLogs];
```

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Aufzeichnung von Nutzungsanalysedaten aktivieren
IMFAnalytics.sharedInstance().setEnabled(true)

// Aufzeichnung von Anwendungslebenszyklusereignissen starten
IMFAnalytics.sharedInstance().startRecordingApplicationLifecycleEvents()


// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
IMFAnalytics.sharedInstance().sendPersistedLogs()
```

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Aufzeichnung von Nutzungsanalysedaten aktivieren
MFPAnalytics.enable();

// Aufgezeichnete Nutzungsanalysedaten an den {{site.data.keyword.amashort}}-Service senden
MFPAnalytics.send();
```
**Anmerkung:** Wenn Sie Cordova-Anwendungen entwickeln, verwenden Sie die native API, um die Aufzeichnung von Anwendungslebenszyklusereignissen zu aktivieren.
