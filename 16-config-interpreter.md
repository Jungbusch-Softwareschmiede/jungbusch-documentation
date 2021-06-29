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
