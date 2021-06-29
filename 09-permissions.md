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
