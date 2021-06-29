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
