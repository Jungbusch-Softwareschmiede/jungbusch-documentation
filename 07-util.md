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
Führt einen Befehl aus

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
Registry Abfrage ausführen

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
