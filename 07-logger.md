# logger

## Description

Dieses package übernimmt das Schreiben der Log-Datei, das Ausgeben von
Informationen auf der Konsole, sowie das Behandeln von Error-Nachrichten und das
Beenden des Programms.

## Usage

```go
var (
	l     logger
	info  level
	warn  level
	erro  level
	debug level
	none  level
)
```

### type level

In diesem struct können die verfügbaren Log-Level gespeichert werden


```go
type level struct {
	name string
	lv   int
}
```
### func  getLevel

```go
func getLevel(lvl int) level
```
Mappt einem Level vom Typ int ein level-Objekt zu.

### type logger

Das Logger-Objekt, welches im Hintergrund die Log-Datei schreibt


```go
type logger struct {
	cmdVerbosity int      // Die Commandline-Stufe
	logVerbosity int      // Die Log-Stufe
	*log.Logger           // Der Logger selbst
	wait         bool     // True, wenn nach beenden des Programms gewartet werden soll
	file         *os.File // Die Log-Datei
}
```
### func  CloseLogger

```go
func CloseLogger()
```
Schließt den Logger

### func  Debug

```go
func Debug(msg string)
```
Gibt eine Nachricht auf dem Debug-Level aus.

### func  Err

```go
func Err(msg string)
```
Gibt eine Nachricht auf dem Error-Level aus.

### func  ErrAndExit

```go
func ErrAndExit(msg string)
```
Gibt eine Nachricht auf dem Error-Level aus und beendet das Programm.

### func  Exit

```go
func Exit()
```
Löscht den Temp-Ordner und beendet das Programm.

### func  HandleError

```go
func HandleError(err error)
```
Gibt den übergebenen Error aus und beendet das Programm. Unterscheidet zwischen
einem herkömmlichen Error und einem SyntaxError-Objekt.

### func  Info

```go
func Info(msg string)
```
Gibt eine Nachricht auf dem Info-Level aus.

### func  InfoPrint

```go
func InfoPrint(msg string, always bool)
```
Gibt eine Nachricht auf dem Info-Level aus. Wird always auf true gesetzt, wird
die Nachricht auf der Konsole unabhängig vom Log-Level ausgegeben.

### func  InfoPrintAlways

```go
func InfoPrintAlways(msg string)
```
Gibt eine Nachricht auf dem Info-Level aus. Die Nachricht auf der Konsole wird
unabhängig vom Log-Level ausgegeben.

### func  InitializeLogger

```go
func InitializeLogger(cs *ConfigStruct, preLog []LogMsg) error
```
Initialisiert alle für die Verwendung des Loggers intern benötigten Werte

### func  InitializeOutput

```go
func InitializeOutput(cs *ConfigStruct) (err error)
```
Initialisiert den Output-Ordner. In diesem wird die Log-Datei abgelegt.

### func  LogPanic

```go
func LogPanic(cs *ConfigStruct, preLog []LogMsg)
```
Diese Funktion wird dann aufgerufen, wenn vor Initialisierung des Loggers ein
Fehler aufgetreten ist. Es wird versucht eine Log-Datei an unterschiedlichen
Pfaden zu erstellen, bis dies erfolgreich ist.

### func  Seperate

```go
func Seperate() string
```
Returned eine Linie

### func  SeperateTitle

```go
func SeperateTitle(in string) string
```
Der übergebene String wird zwischen Linien gesetzt

### func  Warn

```go
func Warn(msg string)
```
Gibt eine Nachricht auf dem Warn-Level aus.

### func  createSyntaxErrorString

```go
func createSyntaxErrorString(keyword string, lineNumber int, line string) string
```
Diese Methode erstellt einen Error-String, der einen benutzerdefinierte
Nachricht, sowie, wenn möglich, die genaue Position des Errors ausgiebt.

### func  logMe

```go
func logMe(msg string, verbosity level, alwaysPrint bool)
```
Übernimmt die Logik des Ausgeben der Nachrichten, sowie die Progressbar

### func  panicExit

```go
func panicExit(cs *ConfigStruct, preLog []LogMsg) (string, error)
```
Hält die Logik für die LogPanic-Methode

### func  processPrelogMsg

```go
func processPrelogMsg(msg LogMsg)
```
Verarbeitet die übergebenen LogMsg-Objekte des PreLoggers. Wenn die Nachricht
vom Typ Error ist, wird sie ausgegeben und das Programm beendet, ansonsten wird
sie wie gewohnt auf dem korrekten Level ausgegeben.
