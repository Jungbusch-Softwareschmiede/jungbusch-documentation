# Jungbusch-Auditorium: Dokumentation

Dieses Repository enthält die Dokumentation für das Jungbusch-Auditorium. Für eine HTML/PDF-Version, siehe [Releases](https://github.com/Jungbusch-Softwareschmiede/jungbusch-documentation/releases). Für zugehörige Repositories, siehe [Jungbusch-Overview](https://github.com/Jungbusch-Softwareschmiede/jungbusch-overview).

----

# Kurzübersicht

## Verzeichnisbaum

jungbusch-auditorium  
    ├── [audit.jba](#audit.jba)  
    ├── [config.ini](#config.ini)  
    ├── [main.go](#main.go)  
    ├── auditorium  
        ├── auditconfig  
            ├── [acutil](#acutil)  
                ├── syntax.go  
                └── util.go  
            ├── [interpreter](#interpreter)  
                ├── audit_interpreter.go  
                └── audit_validator.go  
            ├── [parser](#parser)  
                └── parser.go  
            └── [syntaxchecker](#syntaxchecker)  
                └── syntaxchecker.go  
        ├── config  
            ├── [config-interpreter](#config-interpreter)  
                └── config_interpreter.go  
            └── [config-parser](#config-parser)  
                ├── config_parser.go  
                └── config_parser_flags.go  
        ├── [modulecontroller](#modulecontroller)  
            ├── module_controller.go  
            └── os_detector.go  
        └── [outputgenerator](#outputgenerator)  
            └── output_generator.go  
    ├── [models](#models)  
        ├── cli.go  
        ├── dot_jba.go  
        └── module.go  
    ├── [modules](#modules)  
        ├── grep.go  
        ├── modprobe.go  
        ├── win_registry_query.go  
        └── ..  
    ├── [static](#static)  
        └── static.go  
    ├── [test](#test)  
        └── ..  
    └── [util](#util)  
        ├── [logger](#logger)  
            └── logger.go  
        ├── [permissions](#permissions)  
            ├── unix_permissions.go  
            └── windows_permissions.go  
        ├── [privilege](#privilege)  
            ├── privilege_detector_unix.go  
            └── privilege_detector_windows.go  
        ├── unix_utility.go  
        ├── utility.go  
        └── windows_utility.go  

### audit.jba
In der `audit.jba` werden die Auditschritte mit den Bedingungen und den zugehörigen Modulen definiert.

### config.ini
In der `config.ini` werden allgemeine Programmeinstellungen gesetzt wie z.B. der Pfad zur Audit-Konfigurationsdatei.

### main.go
Die `main.go` Datei wird beim Programmstart ausgeführt und ruft die einzelnen Programmteile auf.

### auditcfg
Der `syntaxchecker.go` überprüft den Syntax der Audit-Konfigurationsdatei und `parser.go` liest die Datei in AuditModule-Objekte ein. Diese werden an `audit_interpreter.go` weitergegeben.

### acutil
Hier werden wiederkehrende Funktionen ausgelagert, die für das Parsen und Validieren der Auditconfig von Relevanz sind.

### interpreter
Hier werden die vom Parser übergebenen Module im `audit_validator.go` auf ihre Gültigkeit geprüft daraufhin im `audit_interpreter.go` ausgeführt.

### parser
Der `parser.go` übersetzt die einzelnen Auditschritte in ein Slice aus AuditModule-structs.

### syntaxchecker
Der `syntaxchecker.go` prüft ob der Syntax der Auditkonfigurationsdatei valide ist.

### config-parser
Der `config_parser.go` erstellt aus den angegbenen Commandline-Parametern und der Config-Datei ein ConfigStruct-Objekt. 

### config-interpreter
Der `config_interpreter.go` wird die vorher eingelesene Konfiguration interpretiert und validiert.

### modulecontroller
Der `module_controller.go` bildet die Verbindung zwischen dem Framework und den Modulen.
Der `os_detector.go` erkennt das aktuelle Betriebsystem. 

### outputgenerator
Der `output_generator.go` speichert Artefakte, erstellt den Abschlussbericht und zippt gegebenfalls den gesamten Output.

### models
Hier werden structs ausgelagert.

### modules
Hier befinden sich alle Module für die unterschiedlichen Betriebsysteme. 

### static
In `static.go` werden alle Konstanten des Programms ausgelagert.

### test
Dieses Verzeichnis beinhaltet Tests für einzelne Datein und deren zugehörigen Assets.

### util
In den verschiedenen `utility.go` Dateien werden wiederkehrende Funktionen zusammengefasst. 

### logger
Der `logger.go` übernimmt Konsolen-Ausgaben und schreibt diese kontinuierlich in eine Logdatei im Output-Ordner.

### permissions
Hier werden die Lese-, Schreib- und Zugriffsrechte einer Datei oder eines Verzeichnisses geprüft.

### privilege
Hier wird überprüft, ob das Jungbusch-Auditorium mit Root-/Admin-Rechten gestartet wurde.

# Installation und Kompilieren

## Vorraussetzungen

- [GoLang](https://golang.org/dl/) nach der offiziellen Installationsanleitung auf dem System installiert

## Einrichten der Projektumgebung

Ist die Go-Umgebungsvariable korrekt gesetzt, kann mit dem Befehl `go env GOPATH` der Go-Pfad ausgegeben werden. Existiert der `go`-Ordner noch nicht, sollte dieser erstellt werden. 

Im Go-Ordner sollte nun der `src`-Ordner erstellt werden, darin ein `github.com`-Ordner und darin wiederum ein ein Ordner mit dem Name `Jungbusch-Softwareschmiede`. Hier kann nun das Github-Projekt geklont werden. Im gesamten sollte die Ordnerstruktur wie folgt aussehen: 

`%gopath%\src\github.com\Jungbusch-Softwareschmiede\jungbusch-auditorium`

## Kompilieren des Projekts

### Windows

Das Kompilieren kann entweder mit einer externen Projektumgebung, wie beispielsweise [GoLand](https://www.jetbrains.com/go/) von JetBrains oder direkt über die Commandline ohne zusätzliche Programme geschehen.

Zum Kompilieren per Commandline, wird zunächst eine Eingabeaufforderung im Pfad des `jungbusch-auditorium`-Ordners geöffnet. 

Daraufhin wird der Befehl `go get github.com/josephspurrier/goversioninfo/cmd/goversioninfo` ausgeführt. Dieses Package wird zur Generierung der `File-Properties`/`Version-Info`, bzw. dem setzen des Icons verwendet.

Als nächstes wird der Befehl `go generate` ausgeführt. Beim ersten Ausführen werden alle benötigten Packages heruntergeladen und es wird eine `resource.syso`-Datei mit dem Icon und der Versioninfo generiert.

Als letztes wird der Befehl `go build` ausgeführt. Es wird eine ausführbare Datei für Windows im Pfad des `jungbusch-auditoriums` generiert.

### Linux/Darwin

Zum Kompilieren auf Linux wird ein Terminal im Ordner `jungbusch-auditorium` geöffnet und der Befehl `go build` ausgeführt. Gegebenenfalls müssen nach dem Klonen die Berechtigungen des Ordners angepasst werden. Beim ersten Ausführen werden alle benötigten Packages heruntergeladen.

## Betriebssystemübergreifendes Kompilieren

Siehe auch: [Go-Wiki auf Github](https://github.com/golang/go/wiki/WindowsCrossCompiling)

### Linux -> Windows

Zum Kompilieren von Windows-Executables, wenn man sich auf Linux befindet, öffnet man wie gewohnt ein Terminal im Pfad des `jungbusch-auditorium`-Ordners und führt daraufhin den Befehl `GOOS=windows GOARCH=amd64 go build` aus.

### Windows -> Linux

Zum Kompilieren einer Linux-Executable auf Windows muss zuerst der Befehl `set GOOS=linux` ausgeführt werden. Daraufhin wie gewohnt `go build`. Zuletzt sollte das die GOOS-Variable wieder auf Windows zurückgesetzt werden.

# Externe Libraries

Das Jungbusch Auditorium verwendet einige wenige Libraries, die nicht von GoLang selbst zur Verfügung gestellt werden. Diese sind folgend aufgeführt. 

**Anmerkung:** Alle aufgeführten Libraries verwenden selbst weitere Libraries.

- [progressbar](https://github.com/schollz/progressbar/) von [schollz](https://github.com/schollz), Version 3.8.1, Lizenz: MIT

- [goja](https://github.com/dop251/goja) von [dop251](https://github.com/dop251), Lizenz: MIT

- [errors](https://github.com/pkg/errors), Lizenz: [BSD 2](https://github.com/pkg/errors/blob/master/LICENSE)

# static

## Description

Im Package static werden Konstanten und "Konstanten-ähnliche" Variablen
gesammelt. Dies erlaubt das leichte anpassen vieler Konstanten und dient der
Übersichtlichkeit.

## Usage

```go
const (
	CURRENT_VERSION = "V1.0 (Letzte Änderung: 29.06.2021)"
	PATH_SEPERATOR  = string(os.PathSeparator)

	// Setzt Default-Werte der Programmkonfiguration
	EXPECTED_CONFIG_PATH      string = `./config.ini`
	EXPECTED_AUDIT_PATH       string = `./audit.jba`
	DEFAULT_OUTPUT_PATH       string = `./`
	DEFAULT_LOG_VERBOSITY     int    = 3
	DEFAULT_CONSOLE_VERBOSITY int    = 2

	// Legt fest, welche Methodennamen das Jungbusch-Auditorium in Modulen erwartet.
	// Werden diese Werte angepasst, müssen auch alle bestehenden Module angepasst werden.
	MODULE_INITIALIZER_SUFFIX = "Init"
	MODULE_EXECUTOR_SUFFIX    = ""
	MODULE_VALIDATOR_SUFFIX   = "Validate"

	// Legt den Name der zu erstellenden Log-Datei fest.
	LOG_NAME = "Jungbusch-Auditorium"

	// Legt den Name des zu erstellenden Output-Ordners fest.
	OUTPUT_FOLDER_NAME      = "jba-result"
	OUTPUT_TIMESTAMP_FORMAT = "02-01-06T150405" // Siehe Time.Format

	// Legt fest, welche Strings von den Modulen als Anzeige des Fortschritts ausgegeben werden
	PASSED_OUTPUT       = "Test '%v' PASSED"
	NOTPASSED_OUTPUT    = "Test '%v' NOT PASSED"
	UNSUCCESSFUL_OUTPUT = "Test '%v' UNSUCCESSFUL"
	NOTEXECUTED_OUTPUT  = "Test '%v' not executed"

	// Reg-Ex
	REG_VARIABLE_NAME = "^[A-Za-z0-9_]+$"    // Zeichensatz der in Variablen erlaubt ist
	REG_VARIABLE      = "%([a-zA-Z0-9_]*?)%" // Anhand von diesem Zeichnsatz werden Variablen identifiziert
	REG_MODULE_NAME   = "^[A-Za-z0-9_]+$"    // Zeichensatz der in Modul-Namen/Parameter-Namen oder Aliasen enthalten sein darf

	// Parser Errors
	COMMENTBLOCK_NEVER_CLOSED                = "Ein Kommentarblock wurde nicht ordnungsgemäß geschlossen."
	AUDIT_CONFIG_EMPTY                       = "Die angegebene Audit-Konfigurationsdatei ist leer."
	INVALID_LINE                             = "Die Zeile ist ungültig. Möglicher Grund: "
	MODULE_MISSING_OPENING_BRACKET           = "Die öffnende geschweifte Klammer fehlt."
	MODULE_MISSING_CLOSING_BRACKET           = "Die schließende geschweifte Klammer fehlt."
	MODULE_MISSING_CLOSING_BRACKET_COMMA     = "Die schließende geschweifte Klammer ist ungültig. Möglicherweise fehlt das Komma."
	MODULE_EMPTY                             = "Der Audit-Schritt ist leer."
	MODULE_INVALID_EXPRESSION                = "Ungültiger Ausdruck."
	VARIABLE_INVALID                         = "Der Syntax der Variable ist nicht gültig. Möglicher Grund: "
	VARIABLE_INVALID_NAME                    = "Der Name der Variable ist nicht gültig. Möglicher Grund: "
	VARIABLE_INVALID_VALUE                   = "Der Syntax des Werts der Variable ist nicht gültig."
	MODULE_INVALID_MODULE_NAME               = "Der Name des Moduls ist nicht gültig. Möglicher Grund: "
	MODULE_VALUE_INVALID_MULTILINE           = "Der Wert des Multiline-Parameters ist nicht gültig. Möglicher Grund: "
	MODULE_VALUE_INVALID                     = "Der Wert des Parameters ist nicht gültig. Möglicher Grund: "
	MODULE_VALUE_ALREADY_SET                 = "Dieser Wert darf pro Audit-Schritt nur einmalig gesetzt werden."
	MODULE_MISSING_PARAMETER                 = "Einem Audit-Schritt fehlen folgende zwingend zu setzenden Parameter: "
	MODULE_NOT_FOUND                         = "Das angegebene Modul wurde nicht gefunden. Mögliche Gründe: Das Modul wurde nicht als kompatibel markiert oder das Modul ist nicht mit der aktuellen Architektur kompatibel."
	MODULE_REQUIRED_MODULE_PARAMETER_NOT_SET = "Folgender Modul-Parameter muss zwingend angegeben werden: "
	MODULE_NO_TEXT_BEHIND_MULTILINE          = "Hinter den schließenden Backticks von Multiline-Parametern ist kein Text (Kommentare o.ä.) erlaubt."
	PARAMETER_EMPTY                          = "Der Wert des Parameters ist leer."
	MODULE_INVALID_PARAMETER                 = "Der Parameter ist für dieses Modul nicht definiert."
	GLOBAL_MODULES_NOT_ALLOWED_NESTED        = "Globale Audit-Schritte dürfen keine verschachtelten Audit-Schritte haben. In folgendem Schritt ist ein Fehler aufgetreten: (ID): "
	GLOBAL_MODULE_NESTED                     = "Globale Audit-Schritte dürfen nicht verschachtelt sein. In folgendem Schritt ist ein Fehler aufgetreten: (ID): "
	GLOBAL_VARIABLE_READONLY                 = "Globale Variablen dürfen nur in globalen Audit-Schritten überschrieben werden. In folgendem Schritt ist ein Fehler aufgetreten (ID): "

	// Parser Errors: Gründe
	TOO_MANY_QUOTATIONMARKS                  = "Zu viele Anführungszeichen."
	TOO_MANY_TICKS                           = "Zu viele Backticks."
	MISSING_TICKS                            = "Fehlende Backticks."
	MISSING_QUOTATIONMARKS                   = "Fehlende Anführungszeichen."
	VARIABLE_MISSING_PERCENTAGE              = "Der Variablenname muss von Prozentzeichen umschlossen sein."
	INVALID_CHARACTERS                       = "Es wurden nicht-erlaubte Zeichen verwendet."
	INVALID_SYNTAX_OR_MISSING_QUOTATIONMARKS = "Der Syntax der Bedingung ist nicht valide oder fehlende Anführungszeichen."
	INVALID_VALUE_FOR_BOOL                   = "Der Boolean-Wert ist ungültig. (true/false)"
	ID_ALREADY_USED                          = "IDs müssen einzigartig sein."
	ENVIRONMENT_VARIABLES_READONLY           = "Umgebungsvariablen dürfen nicht überschrieben werden."
	VARIABLE_ALREADY_SET                     = "Diese Variable wurde in diesem Modul bereits gesetzt."
	ROW_IS_END_OF_MODULE                     = " Anmerkung: Die angegebene Zeile ist die schließende Klammer des betreffenden Moduls."
)
```

```go
var (
	// Die Liste der verfügbaren Module. Wird ein neues Modul implementiert, muss es hier hinzugefügt werden.
	Modules = []string{

		"ExecuteCommand",
		"FileContent",
		"IsFile",
		"Grep",
		"Permissions",
		"Script",

		"Auditctl",
		"AwkScript",
		"BashScript",
		"CheckPartition",
		"Modprobe",
		"NftListRuleset",
		"Sshd",
		"Stat",
		"Sysctl",
		"Systemctl",

		"IsInstalled",
		"IsNotInstalled",

		"Authselect",

		"AuditPolicyQuery",
		"DumpSecuritySettings",
		"ExportInstalledSoftware",
		"GetAccountName",
		"GetUserSID",
		"GetWinEnv",
		"IsGPTemplatePresent",
		"RegistryQuery",
		"SecuritySettingsQuery",
	}

	// Legt alle Betriebssysteme fest, die sich in der Linux-Wildcard befinden.
	Linux = []string{
		"ubuntu",
		"debian",
		"centos",
		"rhel",
		"sles",
		"sles_sap",
	}

	// Legt alle Betriebssysteme fest, die sich in der Windows-Wildcard befinden.
	Windows = []string{
		"windows10",
		"windowsserver2012",
		"windowsserver2016",
		"windowsserver2019",
		"windows8",
		"windows7",
		"windowsxp",
	}

	// Legt alle Betriebssysteme fest, die sich in der Darwin-Wildcard befinden.
	Darwin = []string{
		"macos11.0",
		"macos10.15",
		"macos10.14",
	}

	// Über diesen String wird in der Jungbusch-Auditorium Global auf das Ergebnis des OS-Detectors zugegriffen.
	OperatingSystem = ""

	// Über diesen String wird in der Jungbusch-Auditorium Global auf den Pfad des
	// temporären Ordners zugegriffen. (Nur Windows)
	TempPath = ""

	// In diesem Bool wird gespeichert, ob das Jungbusch-Auditorium root, bzw. Administrator-Rechte hat.
	HasElevatedPrivileges = false

	// In dieser Variable wird gespeichert, mit welchen Permissions das Jungbusch-Auditorium Dateien erstellt.
	// Dieser Wert ändert sich, wenn das Auditorium Root-Rechte hat. Siehe: [ConfigStruct](#testxdd)
	CREATE_FILE_PERMISSIONS os.FileMode = 0644

	// In dieser Variable wird gespeichert, mit welchen Permissions das Jungbusch-Auditorium Ordner erstellt.
	// Dieser Wert ändert sich, wenn das Auditorium Root-Rechte hat. Siehe: [ConfigStruct](#testxdd)
	CREATE_DIRECTORY_PERMISSIONS os.FileMode = 0755

	// Speichert den Error, der geworfen wird, wenn ein Registry-Key nicht gefunden wurde. (Windows)
	ERROR_KEY_NOT_FOUND = errors.New("Der angegebene Key konnte nicht gefunden werden!")

	// Speichert den Error, der geworfen wird, wenn eine Registry-Value nicht gefunden wurde. (Windows)
	ERROR_VALUE_NOT_FOUND = errors.New("Die angegebene Value konnte nicht gefunden werden!")

	ProgressBar *progressbar.ProgressBar
)
```
# models

## Description

In diesem Package werden im Jungbusch-Auditorium an unterschiedlichen Stellen
verwendete Datentypen gesammelt. Dies hat den Vorteil, dass so Import-Loops
vermieden werden. Hat das Package `Parser` beispielsweise das struct
`AuditModule` und eine `Utility-Methode` bekommt ein solches Objekt zur
Verwendung der Methode aus dem `Parser` übergeben, dann wurde ein Loop
erschaffen, da Util den Parser wegen des structs importieren muss und der Parser
wiederum Util importiert um die Methode verwenden zu können. Das Programm wird
so nicht kompilieren.

## Usage

### type Artifact

In diesem Datentyp werden von den Modulen generierte Artefakte gespeichert


```go
type Artifact struct {
	Name   string // Der Name des Artefakts
	Value  string // Der Wert des Artefakts
	IsFile bool   `json:"-"` // True, wenn das Artefakt eine Datei ist
}
```
### type AuditModule

In diesem struct wird ein vollständiger Audit-Schritt, gemeinsam mit allen
verschachtelten Modulen gespeichert.


```go
type AuditModule struct {
	Condition                  string        // Die Bedingung, unter welcher das Modul ausgeführt wird.
	ModuleName                 string        // Der Name des Moduls, welches aufgerufen wird. Aliase werden vom Parser zum Name konvertiert.
	Description                string        // Beschreibung des Audit-Schritts.
	StepID                     string        // Eindeutige Identifikation des Audit-Schritts.
	Print                      string        // Variablen und Werte die nach Ausführung des Moduls ausgegeben werden.
	RequiresElevatedPrivileges bool          // Wert kommt aus dem Modul-Initializer. Kann aus der Audit-Konfiguraion überschrieben werden.
	PrivilegesOverwritten      bool          // True, wenn RequiresElevatedPrivileges aus der Audit-Konfiguration überschrieben wurde.
	Passed                     string        // Die Passed-Condition des Audit-Schritts.
	IsGlobal                   bool          // True, wenn der Schritt eine globale Variable enthält
	Variables                  VariableMap   // Eine Map aus allen [Variable](#type-variable), auf die der Audit-Schritt Zugriff hat.
	ModuleParameters           ParameterMap  // Eine Map aus allen Parametern, die für das Modul in der Audit-Konfig angegeben wurde.
	NestedModules              []AuditModule // Alle verschachtelten Audit-Schritte
}
```
### type ConfigStruct



```go
type ConfigStruct struct {
	// Programm-Parameter
	AuditConfig                  string // Der Pfad zur Audit-Konfiguration
	Config                       string // Der Pfad zur config.ini-Datei
	OutputPath                   string // Der Pfad, in welcher der Output-Ordner erstellt wird
	VerbosityLog                 int    // Das Verbositylevel der Log-Datei
	VerbosityConsole             int    // Das Verbositylevel der Konsolenausgaben
	SkipModuleCompatibilityCheck bool   // True, wenn alle Module unabhängig von Kompatibilität geladen werden sollen
	KeepConsoleOpen              bool   // True, wenn beim Doppelclicken auf die Executable das Konsolenfenster nach vollständigem Durchlauf offen bleiben soll
	ForceOS                      string // Mit diesem Parameter kann das Ergebnis des OS-Detectors überschrieben werden
	IgnoreMissingPrivileges      bool   // True, wenn das Programm nicht abbrechen soll, wenn es nicht mit den für die Audit-Konfiguration nötigen Privilegien gestartet wurde
	AlwaysPrintProgress          bool   // True, wenn der Fortschritt in den Modulen unabhängig vom Log-Level ausgegeben werden soll
	Zip                          bool   // True, wenn eine Zip-Datei, zusätzlich zum Output-Ordner erstellt werden soll
	ZipOnly                      bool   // True, wenn eine Zip Datei erstellt, der Output-Ordner aber entfernt werden soll

	// One-And-Done-Parameter (Programm führt keine Audits aus)
	Version             bool   // True, wenn nur der Version-String ausgegeben werden soll
	ShowModule          string // Hier wird ein Modulname übergeben, dessen Informationen ausgegeben werden sollen ("all" für alle Module)
	CheckConfiguration  bool   // True, wenn die Audit-Konfiguration geparsed, aber nicht ausgeführt werden soll
	CheckSyntax         bool   // True, wenn die Audit-Konfiguration ausschließlich auf ihre Syntax geprüft werden soll
	SaveConfiguration   bool   // True, wenn die aktuelle Konfiguration nach dem Parsen in die config.ini geschrieben werden soll
	CreateDefaultConfig bool   // True, wenn die Default-Configuration angelegt werden soll
}
```
### type LogMsg



```go
type LogMsg struct {
	Message     string // Die Log-Nachricht
	Level       int    // Das Log-Level (0=None, Error, Warn, Info, 4=Debug)
	AlwaysPrint bool   // True, wenn die Nachricht unabhängig vom Log-Level ausgegeben werden soll
}
```
### type ModuleResult

In diesem struct sammelt ein Modul seine Ergebnisse


```go
type ModuleResult struct {
	Artifacts []Artifact // Eine Liste aus allen Artefakten des Moduls
	Result    string     // Das Ergebnis des Moduls, beeinflusst vom Grep-Parameter
	ResultRaw string     // Das Ergebnis des Moduls, unverändert
	Err       error      // Ein Error, falls aufgetreten
}
```
### type ModuleSyntax

Mithilfe dieses structs können die Module ihre eigenen Parameter setzen.


```go
type ModuleSyntax struct {
	ModuleName                 string             // Der Name des Moduls
	ModuleAlias                []string           // Eine Liste aus allen Modul-Aliasen
	ModuleDescription          string             // Die Beschreibung des Moduls
	ModuleCompatibility        []string           // Eine Liste aus allen kompatiblen Betriebssystemen oder Wildcards
	RequiresElevatedPrivileges bool               // True, wenn das aktuelle Modul Administrator-/Root-Privilegien benötigt
	InputParams                ParameterSyntaxMap // Eine Map aus erwarteten Input-Parametern
}
```
### type Parameter

In diesem struct werden Parameter gespeichert. Module bekommen Parameter aus der
Audit-Konfiguration übergeben.


```go
type Parameter struct {
	ParamName  string
	ParamValue string
}
```
### type ParameterMap

Alias für [string]string Map


```go
type ParameterMap map[string]string
```
### type ParameterSyntax

Mit diesem struct setzen die Module welche Parameter sie erwarten und in welcher
Form


```go
type ParameterSyntax struct {
	ParamName        string   // Der Name des Parameters
	ParamAlias       []string // Eine Liste mit allen Parameter-Aliasen
	ParamDescription string   // Die Beschreibung des Parameters
	IsOptional       bool     // True, wenn der Parameter nicht zwingend anzugeben ist
}
```
### type ParameterSyntaxMap

Alias für eine Map aus string und Parametersyntax


```go
type ParameterSyntaxMap map[string]ParameterSyntax
```
### type SyntaxError

Syntax-Error-Objekte werden vom Audit-Konfigurations-Parser verwendet.


```go
type SyntaxError struct {
	ErrorMsg     string // Die Error-Nachricht
	LineNo       int    // Die mögliche Zeilen-Nummern des Errors
	Line         string // Der Inhalt der Zeile des Errors
	Errorkeyword string // Das Schlüsselwort, an dem der Error aufgetreten ist, wenn vorhanden
	Err          error  // Ein herkömmlicher Error
}
```
### func (*SyntaxError) Error

```go
func (e *SyntaxError) Error() string
```
Diese Methode ist zuständig für das Parsen eines Syntax-Errors in einen String

### type Variable

In diesem struct werden Variablen aus der Audit-Konfiguration gespeichert.


```go
type Variable struct {
	Name     string
	Value    string
	IsEnv    bool
	IsGlobal bool
}
```
### type VariableMap

Alias für [string]Variable Map


```go
type VariableMap map[string]Variable
```
# util

## Description

## Usage

### func  ArrayContainsString

```go
func ArrayContainsString(arr []string, val string) bool
```
Returned true, wenn der Array den übergebenen String enthält

### func  AuditModulePrinter

```go
func AuditModulePrinter(mod [AuditModule](#type-auditmodule), tabs int)
```
Konsolenausgaben (Debug)

### func  CastToAppropriateType

```go
func CastToAppropriateType(value string) interface{}
```
Castet den übergebenen String entweder zu einem Boolean, Float oder String, wenn
nichts anderes zutrifft

### func  CompressString

```go
func CompressString(in string) string
```
Entfernt alle Leerzeichen in einem String

### func  CreateFile

```go
func CreateFile(data []string, fileName string) error
```
Erstellt eine Datei. Ist dieselbe Datei bereits vorhanden, wird sie
überschrieben.

### func  ExecCommand

```go
func ExecCommand(command string) (string, error)
```
Führt den übergebenen Befehl aus

### func  GetAbsolutePath

```go
func GetAbsolutePath(currentPath string) (path string, err error)
```
Gibt den absoluten Pfad des übergebenen Pfads zurück. Geht vom Pfad der
Executable aus. Die aktuell working-directory wird ignoriert.

### func  GetStringInBetween

```go
func GetStringInBetween(str string, rem string) string
```
Returned den string aus str der zwischen strings (rem) steht

### func  IsDir

```go
func IsDir(name string) bool
```
Gibt true zurück, wenn der übergebene Pfad ein Verzeichniss ist.

### func  IsFile

```go
func IsFile(name string) bool
```
Gibt true zurück, wenn der übergebene Pfad eine Datei ist.

### func  ParseStringToBool

```go
func ParseStringToBool(in string) (bool, error)
```
Parsed den Wert eines übergebenen Strings in einen Boolean und gibt diesen
zurück.

### func  PrintStrArray

```go
func PrintStrArray(in []string) string
```
Gibt den übergebenen string-Array auf der Konsole aus

### func  ReadFile

```go
func ReadFile(filename string) ([]string, error)
```
Liest eine utf-8-Datei ein

### func  ReadUTF16File

```go
func ReadUTF16File(filename string) ([]string, error)
```
Liest eine utf16-Datei ein

### func  RegQuery

```go
func RegQuery(keyPath string, value string) (string, error)
```
Dummy Funktion, wird benötigt da diese Funktion im OS-Detector ausschließlich
für Windows aufgerufen wird und Go meckert wenn sie für Unix nicht vorhanden
ist.

### func  RemoveFromString

```go
func RemoveFromString(in string, toReplace []string) string
```
Entfernt alle im Array übergebenen Strings aus dem String

### func  readFileWorker

```go
func readFileWorker(filename string, mode string) ([]string, error)
```
Hilfs-Funktion zum Einlesen von Dateien
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
# permissions

## Description

Erlaubt das bestimmen von Datei- oder Directory-Permissions basierend auf den
Berechtigungen des aktuellen Prozesses

## Usage

### func  Permission

```go
func Permission(in string) (read bool, write bool, isDir bool, err error)
```
Überprüft die Read/Write-Rechte des ausführenden Users einer Datei oder
Directory

### func  directoryHasRead

```go
func directoryHasRead(in string) (read bool, err error)
```
Überprüft ob der aktuelle User read-Berechtigungen für die angegebene Directory
hat, indem wir die Directory selbst auslesen

### func  directoryHasWrite

```go
func directoryHasWrite(in string) (write bool, err error)
```
Überprüft, ob eine Directory Write-Permissions hat. Es ist möglich dass wir
write haben, aber keine read

### func  fileHasRead

```go
func fileHasRead(in string) (read bool, err error)
```

### func  fileHasWrite

```go
func fileHasWrite(in string) (read bool, err error)
```

### func  fileHelper

```go
func fileHelper(in string, remove bool, args int) (perm bool, err error)
```

### func  getDirectoryPerms

```go
func getDirectoryPerms(dir string) (read bool, write bool, err error)
```
Überprüft die Permissions des ausführenden Users einer Directory Der User kann
read-, aber keine write-Rechte haben - oder andersrum

### func  getFilePerms

```go
func getFilePerms(file string) (read bool, write bool, err error)
```
Überprüft die Permissions des ausführenden Users einer File
# privilege

## Description

Überprüft, ob der auszuführende Nutzer Administrator/ Root-Privilegien hat

## Usage

### func  HasRootPrivileges

```go
func HasRootPrivileges() bool
```
Prüfen ob Prozess als root gestartet wurde
# acutil

## Description

Dieses Package ist ein Utility-Package für das Validieren und Parsen der
Audit-Konfiguration. Alle Methoden des Packages greifen ausschließlich auf die
über die Methode SetLines gesetzte, rohe Audit-Konfigurationsdatei zu und sind
anderweitig nicht zu verwenden.

## Usage

```go
var (
	lines []string // Die Audit-Konfigurationsdatei mit welcher gearbeitet wird
)
```

### func  AreLinesEmpty

```go
func AreLinesEmpty() bool
```
True, wenn die Konfigurationsdatei leer ist.

### func  EvaluateClosingBracketError

```go
func EvaluateClosingBracketError(n *int) error
```
Versucht zu evaluieren, ob sich der Fehler an der übergebenen Zeile auf ein
fehlendes Komma zurückführen lässt.

### func  GenerateSyntaxError

```go
func GenerateSyntaxError(errorMsg string, lineNo int, line string, keyword string) *SyntaxError
```
Generiert einen Error des Typs [SyntaxError](#type-syntaxerror) aus den übergebenen
Informationen.

### func  GetModuleParameterSyntaxNameFromAlias

```go
func GetModuleParameterSyntaxNameFromAlias(moduleSyntax ModuleSyntax, alias string) string
```
Konvertiert einen Modulparameter-Alias in dessen Name anhand vom übergebenen
Modul.

### func  GetModuleSyntaxFromNameOrAlias

```go
func GetModuleSyntaxFromNameOrAlias(name string, modules []ModuleSyntax) (ms ModuleSyntax)
```
Sucht in den übergebenen Modulen anhand des übergebenen Aliases nach dem Name
des Moduls.

### func  GetParameterSyntaxFromKeyword

```go
func GetParameterSyntaxFromKeyword(keyword string) ParameterSyntax
```
Sucht anhand eines Keywords das passende ParameterSyntax-Objekt
(allgemeingültig) und returned es oder ein leeres Objekt, falls nichts gefunden
wurde.

### func  GetVariablesInString

```go
func GetVariablesInString(s string) []string
```
Sucht und returned alle Vorkommnisse von Variablen im übergebenen string

### func  GoToEndOfCommentBlock

```go
func GoToEndOfCommentBlock(n *int)
```
Überspringt einen Kommentarblock.

### func  IsComment

```go
func IsComment(n *int) bool
```
True, wenn die Zeile an der übergebenen Zeilennummer ein Kommentar ist.

### func  IsCommentBlock

```go
func IsCommentBlock(n *int) bool
```
True, wenn die Zeile an der übergebenen Zeilennummer ein Kommentarblock ist.

### func  IsCondition

```go
func IsCondition(in string) bool
```
True, wenn der übergebene String im Format einer Condition ist.

### func  IsParameter

```go
func IsParameter(n *int) bool
```
True, wenn die Zeile an der übergebenen Zeilennummer dem Syntax eines Parameters
entspricht.

### func  IsValue

```go
func IsValue(in string) bool
```
True, wenn der übergebene String dem Format eines Werts entspricht. (Umgeben von
Anführungszeichen)

### func  IsVariable

```go
func IsVariable(in string) bool
```
True, wenn der übergebene String dem Format einer Variable entspricht. (Also von
Prozentzeichen umgeben)

### func  IsVariableAssignment

```go
func IsVariableAssignment(n *int) bool
```
True, wenn die Zeile an der übergebenen Zeilennummer dem Syntax einer
Variablen-Zuweisung entspricht.

### func  LinesFinished

```go
func LinesFinished(n *int) bool
```
True, wenn das Ende der Konfigurationsdatei erreicht wurde.

### func  PrepareLine

```go
func PrepareLine(line string) (string, error)
```
Diese Methode entfernt Inlinekommentare und Leerzeichen oder Tabs am Start des
übergebenen strings und gibt das Ergebnis zurück.

### func  ReadAuditConfiguration

```go
func ReadAuditConfiguration(file string) (lines []string, err error)
```
Liest die übergebene Auditkonfigurationsdatei ein.

### func  RemoveInlineComment

```go
func RemoveInlineComment(in string) (string, error)
```
Entfernt Inline-Kommentare aus dem übergebenen String.

### func  SetLines

```go
func SetLines(l []string)
```
Setzt die Zeilen der Audit-Konfiguration, mit der die Methoden dieses Packages
arbeiten.

### func  SkipEmpty

```go
func SkipEmpty(n *int)
```
Überspringt leere Zeilen.

### func  SkipIrrelevantLines

```go
func SkipIrrelevantLines(lines []string, n *int) error
```
Überspringt für den Parser irrelevante Zeilen. Dies inkludiert leere Zeilen,
Kommentare sowie Kommentarblöcke.

### func  SplitParameter

```go
func SplitParameter(in string) (string, string)
```
Splittet einen Parameter in Name und Wert. Bei einem Multilineparameter wird nur
die erste Zeile returned.

### func  SplitVariable

```go
func SplitVariable(in string) (string, string)
```
Splittet eine Variable in Name und Wert.

### func  Trim

```go
func Trim(in string) string
```
Entfernt alle Leerzeichen und Tabs die vor dem übergebenen String stehen.

### func  VariablesInStringToLower

```go
func VariablesInStringToLower(in string) string
```
Konvertiert die Namen aller Variablen im übergebenen string zu lowercase und
gibt das Ergebnis zurück.

### func  ifSyntax

```go
func ifSyntax() []ParameterSyntax
```
Diese Methode enthält den Syntax einer Bedingung.

### func  parameterSyntax

```go
func parameterSyntax() []ParameterSyntax
```
Diese Methode enthält in statischen Objekten die allgemeingültigen Parameter der
Auditkonfiguration und deren Syntax.
# syntaxchecker

## Description

Dieses Package ist für das Überprüfen des Syntaxes der Audit-Konfigurationsdatei
zuständig.

## Usage

### func  Syntax

```go
func Syntax(lines []string) error
```
Diese Methode überprüft den Syntax der übergebenen Audit-Konfigurationsdatei.
Sie gibt einen Error zurück, der in den Typ [SyntaxError](#type-syntaxerror) gecasted werden
kann.

### func  syntaxCheckModule

```go
func syntaxCheckModule(lines []string, n *int) (err error)
```
Diese Methode überprüft den Syntax eines einzelnen Moduls. Sie wird rekursiv für
verschachtelte Module aufgerufen.

### func  validateParameter

```go
func validateParameter(lines []string, n *int) (err error)
```
Diese Methode validiert den Syntax eines Parameters.

### func  validateParameterName

```go
func validateParameterName(in string) error
```
Diese Methode validiert den Syntax eines Parameter-Namens.

### func  validateParameterValue

```go
func validateParameterValue(value string, lines []string, n *int) (int, error)
```
Diese Methode validiert den Wert eines Parameters.

### func  validateVariableAssignment

```go
func validateVariableAssignment(lines []string, n *int) (err error)
```
Diese Methode validiert den Syntax einer Variablen-Zuweisung.

### func  validateVariableName

```go
func validateVariableName(name string) error
```
Diese Methode validiert den Syntax eines Variablennames.

### func  validateVariableValue

```go
func validateVariableValue(_ string) error
```
Diese Methode validiert den Syntax des Werts einer Variable.
# parser

## Description

Dieses Package ist für das Einlesen der Auditkonfigurations-Datei in
[AuditModule](#type-auditmodule) -Objekte zuständig. Sie ist darauf angewiesen, dass vorher
der Syntaxchecker erfolgreich durchgelaufen ist und somot alle möglichen
Syntaxerror abgefangen wurden. Ist dies nicht der Fall und enthält die
Auditkonfigurationsdatei Fehler, dann ist das Auftreten eines Panics in diesem
Package wahrscheinlich.

## Usage

```go
var (
	processRequiresElevatedPrivileges bool            // Speichert ob der Prozess Administratorprivilegien benötigt.
	numberOfModules                   int             // Enthält die gesamte Anzahl der eingelesenen Module. Wird für die Progressbar benötigt.
	usedIds                           map[string]bool // Mit dieser Map wird gespeichert, welche IDs für die Module bereits verwendet wurde.
	loadedModules                     []ModuleSyntax  // In dieser Map werden die geladenen Modulen für den Zugriff aus dem gesamten Package gespeichert.
)
```

### func  Parse

```go
func Parse(lines []string, moduleSyntax []ModuleSyntax) ([]AuditModule, bool, int, error)
```
Liest die übergebene Auditkonfigurations-Datei anhand der übergebenen geladenen
Modulen ein. Gibt eine Slice aller Audit-Schritte, ob der Prozess
Administratorberechtigungen benötigt, die gesamte Anzahl der Module und
gegebenenfalls einen Error zurück.

### func  generateModule

```go
func generateModule(lines []string, n *int) (AuditModule, error)
```
Generiert ein einzelnes Modul. Wird rekursiv aufgerufen.

### func  getConditionStringFromString

```go
func getConditionStringFromString(condition string) string
```
Returned den Condition-String aus dem übergebenen String. Klammern und
Anführungszeichen werden entfernt.

### func  handleParameter

```go
func handleParameter(lines []string, n *int, currentModule *AuditModule) error
```
Übernimmt das extrahieren, konvertieren und validieren eines Parameters aus der
übergebenen Zeile.

### func  handleVariable

```go
func handleVariable(lines []string, n *int, currentModule *AuditModule) error
```
Übernimmt das extrahieren, konvertieren und validieren einer Variable aus der
übergebenen Zeile.

### func  initializeAuditModule

```go
func initializeAuditModule() AuditModule
```
Diese Methode initialisiert AuditModules mit ihren im Interpreter zu setzenden
Environment-Variables

### func  setValue

```go
func setValue(pointerToSetIn *string, valueToSet string) error
```
Setzt den übergebenen Wert in den übergebenen Pointer und überprüft ob in den
Pointer bereits etwas gesetzt wurde.

### func  validateCompletenessOfModule

```go
func validateCompletenessOfModule(module *AuditModule, lines []string, n *int) error
```
Überprüft, ob alle nötigen Werte im übergebenen Schritt gesetzt sind.

### func  validateGlobals

```go
func validateGlobals(mods []AuditModule) error
```
Validiert globale Variablen, in allen übergebenen Auditschritten und überprüft
ob sie an der richtigen Stelle deklariert sind und dem geforderten Syntax
entsprechen.
# interpreter

## Description

## Usage

### type moduleVariable

In diesem Struct werden die in Audit-Schritten verwendeten Variablen
gespeichert. Dafür muss der originale Name (also mit %-Zeichen etc.) für später
gespeichert werden und ein neuer Name, der dem ECMAScript-Syntax entspricht,
erzeugt werden.


```go
type moduleVariable struct {
	name     string
	origName string
	value    string
}
```
### func  extractVars

```go
func extractVars(cond string) (v []*moduleVariable)
```
extractVars extrahiert alle Variablen aus der Condition und gibt sie als Array
zurück

### func  InterpretAudit

```go
func InterpretAudit(audit []AuditModule, numberOfModules int, alwaysPrintProgress bool) (report [][ReportEntry](#type-reportentry), err error)
```
Diese Funktion dient als eine Art Wrapper für das Interpretieren der
Audit-Konfiguration. Es wird die Gültigkeit aller Variablen und Parameter
überprüft, auch ob jeder Variable früher oder später ein Wert zugewiesen wird.
Daraufhin werden alle Module ausgeführt und die Ergebnisse in einer Slice aus
[ReportEntry](#type-reportentry)-Objekten zurückgegeben.

### func  ValidateParameters

```go
func ValidateParameters(mods []AuditModule) error
```
Dient als "Start-Funktion". Ruft validateParametersInModule für alle Level-0
Module auf

### func  addNotExecutedToProgressBar

```go
func addNotExecutedToProgressBar(m AuditModule)
```
Fügt Schritte, die, warum auch immer nicht ausgeführt, z.B. weil das Elternmodul
fehlgeschlafen ist, werden der Progressbar als "fertig" zu.

### func  checkExecuteCondition

```go
func checkExecuteCondition(m AuditModule) (bool, error)
```
Überprüft die Ausführ-Bedingung, des Moduls, wenn angegeben

### func  execute

```go
func execute(m AuditModule) (res ModuleResult, err error)
```
Führt die Execute-Methode des übergebenen Moduls aus.

### func  executeModules

```go
func executeModules(modules []AuditModule, numberOfModules int, alwaysPrintProgress bool) [][ReportEntry](#type-reportentry)
```
executeModules führt die in der Audit-Datei festegelegten Module aus und gibt
einen Report zurück. Zuächst wird überprüft, ob die zum Ausführen des Moduls
benötigten Berechtigungen vorliegen. Anschließend wird die Ausführ-Bedingung
überprüft. Ist diese erfüllt, so wird das Modul ausgeführt und das Ergebnis in
ein [ReportEntry](#type-reportentry)-Objekt geschrieben.

### func  handleUnsuccessful

```go
func handleUnsuccessful(m AuditModule, reportEntry *[ReportEntry](#type-reportentry), alwaysPrintProgress bool, err error)
```
Übernimmt das Zusammenbauen eines Report-Entries für einen Audit-Schritt, in dem
ein Fehler aufgetreten ist.

### func  interpretCondition

```go
func interpretCondition(cond string, varMap VariableMap) (bool, error)
```
Interpretiert die übergebene Bedingung mithilfe von GOJA unter Verwendung aller
übergebenen Variablen.

### func  replaceVariablesInString

```go
func replaceVariablesInString(s string, variables VariableMap) string
```
Ersetzt alle Variablen im übergebenenen String mit dem Wert der passenden
Variable, wenn in der übergebenenen Map vorhanden. Löst außerdem Pfade auf.

### func  setPassed

```go
func setPassed(m *AuditModule) error
```
Interpretiert die Passed-Condition, macht Konsolenausgaben und setzt
Umgebungsvariablen

### func  setVarValues

```go
func setVarValues(vars []*moduleVariable, varMap VariableMap) error
```
setVarValues weist den extrahierten Variablen den passenden Wert aus dem Modul
zu

### func  setVariables

```go
func setVariables(m *AuditModule, globalVars *[]Variable) error
```
Iteriert über die Variablen des übergebenen Moduls. Die Werte aller Variablen,
die keine Umgebungsvariablen sind, werden an die Kinder des Moduls
weitergegeben, da Variablen des Elternteils dort ebenfalls zugreifbar sind.

### func  validateVariables

```go
func validateVariables(modules []AuditModule) error
```
Überprüft, ob alle referenzierten Variablen vor Verwendung deklariert wurden
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
# config_interpreter

## Description

In diesem Package wird die vorher eingelesene Konfiguration interpretiert und
validiert. Das bedeutet, dass Parameter ohne Programmstart abgearbeitet werden
und die angegebenen Pfade validiert werden.

## Usage

### func  InterpretConfig

```go
func InterpretConfig(cs *ConfigStruct) (continueExecution bool, err error)
```
Diese Methode bekommt den Pointer zu einem ConfigStruct übergeben. Sie arbeitet
ausstehende Parameter ab und validiert den Pfad zu der Audit-Konfiguration,
sowie den Output-Pfad. Wenn keine Errors auftreten, gibt sie den Boolean
continueExecution zurück. Ist dieser false, wird das Programm nach dem Ausführen
dieser Methode beendet. Das ist beispielsweise dann der Fall, wenn nur die
Version ausgegeben werden soll.

### func  ValidateOutputPath

```go
func ValidateOutputPath(cs *ConfigStruct) (err error)
```
Diese Methode validiert den Output-Pfad. Dafür wird überprüft ob der Pfad
existiert und ob der Prozess Lese- und Schreibrechte hat.

### func  validateAuditConfigPath

```go
func validateAuditConfigPath(cs *ConfigStruct) (err error)
```
Diese Methode validiert den Pfad zur Audit-Konfiguration. Dafür wird überprüft
ob der Pfad existiert und ob der Prozess Lese- und Schreibrechte hat. Des
Weiteren wird überprüft, ob die angegebene Datei vom korrekten Typ ist.

### func  writeStructToConfigFile

```go
func writeStructToConfigFile(cs ConfigStruct, path string) error
```
Diese Methode schreibt ein ConfigStruct in die Datei am übergebenen Pfad. Es
werden nur Parameter in die Datei geschrieben, die keinen leeren Wert haben.
# modulecontroller

## Description

Dieses Package übernimmt die Kommunikation zwischen dem Rest des Frameworks und
der Module. Das Framework ist von den Modulen vollständig getrennt, insofern
dass die Methoden der Module nie explizit aus dem Code aufgerufen wird. Die
einzige Referenz auf die Module befinden sich in der Slice [Modules](#static).
Stattdessen wird Reflection verwendet um die Methoden der Module aufzurufen.
Dafür ist es nötig, dass alle Modul-Methoden einheitliche Namen haben. Welche
Methodennamen erwartet werden, wird von static.MODULE_INITIALIZER_SUFFIX,
static.MODULE_EXECUTOR_SUFFIX und static.MODULE_VALIDATOR_SUFFIX. Die
Methodennamen setzen sich durch den Modulname und den Suffix zusammen.

## Usage

```go
var (
	loadedModules []ModuleSyntax // Speichert alle geladenen Module
)
```

### func  Call

```go
func Call(functionName string, m AuditModule) ModuleResult
```
Wird zum Aufrufen der Hauptmethode (Execute) eines Moduls verwendet werden.
Diese Methode parsed die zu übergebenden Werte, sowie die Rückgabewerte in den
korrekten Datentyp.

### func  CallValidate

```go
func CallValidate(functionName string, params ParameterMap) error
```
Wird zum Aufrufen der Validate-Methode eines Moduls verwendet werden. Diese
Methode parsed die zu übergebenden Werte, sowie die Rückgabewerte in den
korrekten Datentyp. Ist der zurückgegebene Error nil, sind alle Parameter
valide.

### func  GetModuleSyntax

```go
func GetModuleSyntax(module string) string
```
Sucht den Modul-Syntax für den Übergebenen Modul-Name oder Modul-Alias und gibt
diesen als formatierten String zurück.

### func  GetOS

```go
func GetOS() (string, error)
```
Versucht das Betriebssystem und seine Version zu bestimmen. Es wird nicht
zwischen den unterschiedlichen Ausführungen von einzelnen Windows-Versionen
(Home/Pro) etc. unterschieden.

### func  Initialize

```go
func Initialize(skipCompatibilityCheck bool) ([]ModuleSyntax, error)
```
Initialisiert alle Module und überprüft währenddessen, ob die Module mit dem
aktuellen OS kompatibel sind, und alle benötigten Methoden implementieren. Wenn
ja, wird der Syntax des Moduls ([ModuleSyntax](#type-modulesyntax)) in die Slice loadedModules
geschrieben. Mit `skipCompatibilityCheck` kann die Kompatibilitätsüberprüfung
übersprungen werden.

### func  ValidateAuditModules

```go
func ValidateAuditModules(mod []AuditModule) error
```
Überprüft für alle übergeben [AuditModule](#type-auditmodule)-Objekte ob das referenzierte
Modul eine Validate-Methode hat. Wenn ja, wird diese mit den in der
AuditKonfiguration angegebenen Parametern aufgerufen.

### func  callFunctionFromString

```go
func callFunctionFromString(function string, values []reflect.Value) []reflect.Value
```
Ruft die Methode mit dem übergebenen Name und den übergebenen Übergabewerten
auf. Gibt Rückgabewerte in einer Slice im Format reflect.Value zurück, die
zurück in den richtigen Datentyp gecasted werden muss.

### func  doesMethodExist

```go
func doesMethodExist(function string) bool
```
Überprüft ob eine Methode mit dem übergebenen Name in Sichtweite des
[MethodHandler](#type-methodhandler)-Objekts existiert.

### func  getModuleDescription

```go
func getModuleDescription(module ModuleSyntax) string
```
Formatiert den [ModuleSyntax](#type-modulesyntax) eines Moduls in einen string.

### func  hasDisallowedCharacters

```go
func hasDisallowedCharacters(in string) bool
```
True, wenn im übergebenen String für einen Modulname ungültige Zeichen enthalten
sind.

### func  parseParameterSliceToReflect

```go
func parseParameterSliceToReflect(in ParameterMap) []reflect.Value
```
Parsed eine [ParameterMap](#type-parametermap) in mit Reflect zu verwendenden Reflect-Values.

### func  parseReflectToError

```go
func parseReflectToError(in []reflect.Value) error
```
Parsed den Rückgabewert eines Calls in ein Error-Struct.

### func  parseReflectToModuleResult

```go
func parseReflectToModuleResult(in []reflect.Value) ModuleResult
```
Parsed den Rückgabewert eines Calls in ein [ModuleResult](#type-moduleresult)-Struct.

### func  parseReflectToModuleSyntax

```go
func parseReflectToModuleSyntax(in []reflect.Value) ModuleSyntax
```
Parsed den Rückgabewert eines Calls zurück in [ModuleSyntax](#type-modulesyntax).

### func  parseVariableMapToReflect

```go
func parseVariableMapToReflect(pm ParameterMap, vm *VariableMap) []reflect.Value
```
Parsed eine [ParameterMap](#type-parametermap), sowie [VariableMap](#type-variablemap) in mit Reflect zu
verwendenden Reflect-Values.

### func  sanityCheck

```go
func sanityCheck(mod []ModuleSyntax) error
```
Diese Methode überprüft, ob sich die in den Initialize-Methoden von Modulen
gesetzten Namen und Aliase überschneiden. Modulnamen müssen einzigarig sein. Ist
das nicht der Fall, wird ein passender Error geworfen.

### func  validateModule

```go
func validateModule(mod AuditModule) error
```
Überprüft ob das im [AuditModule](#type-auditmodule)-Objekt (also ein Audit-Schritt)
aufgerufene Modul die Validate-Methode implementiert. Wenn ja, wird sie mit den
gegebenen Parametern aufgerufen. Des Weiteren werden die Validate-Module von
Kindern des übergebenen Audit-Schritts ausgeführt. Sind alle Parameter laut den
Validate-Methoden valide wird nil zurückgegeben, ansonsten ein Error.

### func  wildcardCompatibilityCheck

```go
func wildcardCompatibilityCheck(moduleCompatibility []string) bool
```
Überprüft die Modul-Kompatibilität mit Wildcards gegeben ist
# outputgenerator

## Description

## Usage

### type Metadata



```go
type Metadata struct {
	Os           string        `json:"os"`
	Root         bool          `json:"root"`
	Total        int           `json:"total"`
	Passed       int           `json:"passed"`
	Notpassed    int           `json:"not_passed"`
	Unsuccessful int           `json:"unsuccessful"`
	Notexecuted  int           `json:"not_executed"`
	Started      string        `json:"started"`
	Elapsed      string        `json:"elapsed"`
	Report       []ReportEntry `json:"report"`
}
```
### type ReportEntry



```go
type ReportEntry struct {
	ID        string            `json:"id"`
	Desc      string            `json:"desc"`
	Print     string            `json:"print,omitempty"`
	Artifacts []models.Artifact `json:"artifacts"`
	Expected  string            `json:"expected,omitempty"`
	Actual    string            `json:"actual,omitempty"`
	Error     string            `json:"error,omitempty"`
	Result    string            `json:"result"`
	Nested    []ReportEntry     `json:"nested,omitempty"`
}
```
### func  cleanArtifacts

```go
func cleanArtifacts(report []ReportEntry) []ReportEntry
```

### type stats



```go
type stats struct {
	total        int
	passed       int
	notpassed    int
	unsuccessful int
	notexecuted  int
}
```
### func  getStats

```go
func getStats(report []ReportEntry, numberOfModules int) (s stats)
```

### func  GenerateOutput

```go
func GenerateOutput(report []ReportEntry, outputPath string, numberOfModules int, zip bool, start time.Time, elapsed time.Duration) error
```
GenerateOutput erstellt den Report und speichert die Artefakte am spezifizierten
Pfad.

### func  generateReport

```go
func generateReport(report []ReportEntry, outputPath string, numberOfModules int, start time.Time, elapsed time.Duration) (err error)
```

### func  saveArtifacts

```go
func saveArtifacts(report []ReportEntry, outputPath string) error
```

### func  zipFolder

```go
func zipFolder(folder string) error
```
# Informationen und Kontakt

[Relevante Repositories](https://github.com/Jungbusch-Softwareschmiede/jungbusch-overview)

## Kontakt

Rechtschreibfehler können gerne per Issue im Repo des Jungbusch-Auditoriums oder per E-Mail gemeldet werden.

[1924338@stud.hs-mannheim.de](mailto:1924338@stud.hs-mannheim.de)

[hi@marius.codes](mailto:hi@marius.codes)

## Das Projekt 

Dieses Projekt wurde im Rahmen des Projektsemesters im Studiengang [Cybersecurity](https://www.hs-mannheim.de/studieninteressierte/unsere-studiengaenge/bachelorstudiengaenge/cyber-security.html) an der [Hochschule Mannheim](https://www.hs-mannheim.de/) im Zeitraum von 03/2021 - 07/2021 entwickelt.

## Mitwirkende 

Christian Höfig [Mail*](mailto:1920769@stud.hs-mannheim.de) [Github](https://github.com/cookieChrissi) 

Tim Philipp [Mail*](mailto:1921637@stud.hs-mannheim.de) [Github](https://github.com/TimPhi) 
 
Marius Schmalz [Mail*](mailto:1924338@stud.hs-mannheim.de) [Github](https://github.com/ByteSizedMarius) 
 
Felix Klör [Mail*](mailto:1924300@stud.hs-mannheim.de) [Github](https://github.com/prefixFelix) 
 
Tobias Nöth [Mail*](mailto:1925165@stud.hs-mannheim.de) [Github](https://github.com/Tobias01101110) 
 
Lukas Hagmaier [Mail*](mailto:1926235@stud.hs-mannheim.de) [Github](https://github.com/Lucky-180) 

\* Gültig, solange die Person immatrikuliert ist
