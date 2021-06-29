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
