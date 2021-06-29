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
