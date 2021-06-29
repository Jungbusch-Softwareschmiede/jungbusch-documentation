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
