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

