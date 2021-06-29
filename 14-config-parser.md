# config_parser

## Description

Dieses Package verwaltet die Commandline-Flags, sucht und liest eine
Konfigurations-Datei ein und liefert ein Objekt vom Typ [ConfigStruct](#type-configstruct) mit
allen gesetzten Werten zurück. Eine Besonderheit des Packages ist, dass es
anders als alle anderen JBA-Packages nicht den Logger verwendet sondern
stattdessen ein Slice aus models.LogMsg-Objekten zurückgibt. Dies liegt daran,
dass der von anderen Packages verwendete Logger erst nach dem Parsen der
Konfiguration initialisiert werden kann, da hier beispielsweise das Log-Level
gesetzt wird. Daher werden Log-Einträge "gesammelt" und bei der Initialisierung
des Loggers sozusagen nachträglich in den Log geschrieben.

## Usage

```go
var (
	tempLogger []LogMsg
	flags      []cliFlag
)
```

```go
var (
	// Programm-Parameter
	auditConfig_Flag                  string
	config_Flag                       string
	outputPath_Flag                   string
	verbosityLog_Flag                 int
	verbosityConsole_Flag             int
	skipModuleCompatibilityCheck_Flag bool
	keepConsoleOpen_Flag              bool
	forceOS_Flag                      string
	ignoreMissingPrivileges_Flag      bool
	zip_Flag                          bool
	zipOnly_Flag                      bool

	// One-And-Done-Parameter (Programm führt keine Audits aus)
	version_Flag             bool
	createDefaultConfig_Flag bool
	showModules_Flag         bool   // Alle Module (bool)
	showModuleInfo_Flag      string // Ein einzelnes Modul (string)
	checkConfiguration_Flag  bool
	checkSyntax_Flag         bool
	alwaysPrintProgress_Flag bool

	// Misc
	saveConfiguration_Flag bool // Speichern der Commandline-Parameter in Config
)
```
Beschreibung der einzelnen Parameter: Siehe [ConfigStruct](#type-configstruct)

### type cliFlag

In diesem Struct werden die Beschreibungen für die Commandline-Flags
gespeichert, die für das Anzeigen der Usage-Page benötigt werden


```go
type cliFlag struct {
	name     string
	desc     string
	datatype string
}
```
### func  LoadConfig

```go
func LoadConfig() (ConfigStruct, []LogMsg)
```
Diese Methode ist die erste Methode, die im Jungbusch-Auditorium aufgerufen
wird. Sie erzeugt ein [ConfigStruct](#type-configstruct)-Objekt mit den in static definierten
Default-Werten. Ein Pointer zu diesem Objekt wird dann an die
configHandler-Methode übergeben, welche die gesetzten Werte mit denen aus der
config.ini-Datei überschreibt. Daraufhin wird die commandlineHandler-Methode mit
demselben Pointer aufgerufen, welche alle auf der Commandline angegebenen
Parameter parsed und in das Struct setzt.

### func  ResetFlags

```go
func ResetFlags()
```
Wird aufgrund eines Golang-Quirks in den Tests benötigt

### func  add

```go
func add(msg LogMsg)
```
Wrapper für Slice-Append

### func  argsContainFlag

```go
func argsContainFlag(in string) bool
```

### func  commandlineHandler

```go
func commandlineHandler(cs *ConfigStruct) (err error)
```
Diese Funktion nimmt ein ConfigStruct entgegen, welches mit Werten aus der
Konfigurations-Datei und/oder Default-Werten gefüllt ist. Diese Werte werden nun
von den per Commandline angegebenen Parametern überschrieben, wenn vorhanden.

### func  configHandler

```go
func configHandler(cs *ConfigStruct) (err error)
```
Diese Funktion nimmt ein ConfigStruct entgegen, welches bisher nur mit
Default-Werten gefüllt ist. Es wird eine Konfigurations-Datei gesucht und
eingelesen. Für eine Beschreibung, welche Konfigurations-Datei eingelesen wird,
siehe Handbuch

### func  findAuditConfigs

```go
func findAuditConfigs(cs *ConfigStruct) error
```
Diese Funktion findet am Pfad der Executable alle Dateien, welche die
Dateiendung .jba haben. Wenn genau eine jba-Datei gefunden und keine andere
explizit angegeben ist, wird diese automatisch vom Programm verwendet.

### func  getLogLevelFromString

```go
func getLogLevelFromString(in string) (int, error)
```
Konvertiert das übergebene Loglevel (String) in einen int

### func  initializeFlag

```go
func initializeFlag()
```
Diese Methode initialisiert die Flags der Commandline, enthält die
Beschreibungen der Flags, sowie die Help-Page

### func  parseAndSetBool

```go
func parseAndSetBool(toSet *bool, value string) (err error)
```
Parsed den Wert eines übergebenen Strings in einen Boolean und setzt das
Ergebnis in den übergebenen boolean-Pointer. Verwendet parseStringToBool.

### func  readConfigFile

```go
func readConfigFile(cs *ConfigStruct) (err error)
```
Liest die übergebene Konfigurations-Datei vom System ein. Dabei werden Fehler
erzeugt, wenn Key oder Wert fehlen, oder wenn ein ungültiger Key angegeben
wurde. Alle Werte werden in das übergebene ConfigStruct geschrieben.

### func  setCliParameters

```go
func setCliParameters(cs *ConfigStruct) (err error)
```
In dieser Funktion werden die Werte aller Commandline-Parameter ausgelesen, ggf.
in den korrekten Datentyp konvertiert und in das Config-Struct gesetzt
