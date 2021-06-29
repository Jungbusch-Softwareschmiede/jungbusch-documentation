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

