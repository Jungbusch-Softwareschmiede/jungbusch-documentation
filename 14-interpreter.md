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
