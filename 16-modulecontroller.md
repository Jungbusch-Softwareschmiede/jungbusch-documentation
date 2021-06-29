# modulecontroller

## Description

Dieses Package übernimmt die Kommunikation zwischen dem Rest des Frameworks und
der Module. Das Framework ist von den Modulen vollständig getrennt, insofern
dass die Methoden der Module nie explizit aus dem Code aufgerufen wird. Die
einzige Referenz auf die Module befinden sich in der Slice [Modules](#static).
Stattdessen wird Reflection verwendet um die Methoden der Module aufzurufen.
Dafür ist es nötig, dass alle Modul-Methoden einheitliche Namen haben. Welche
Methodennamen erwartet werden, wird von static.MODULE_INITIALIZER_SUFFIX,
static.MODULE_EXECUTOR_SUFFIX und static.MODULE_VALIDATOR_SUFFIX. Die
Methodennamen setzen sich durch den Modulname und den Suffix zusammen.

## Usage

```go
var (
	loadedModules []ModuleSyntax // Speichert alle geladenen Module
)
```

### func  Call

```go
func Call(functionName string, m AuditModule) ModuleResult
```
Wird zum Aufrufen der Hauptmethode (Execute) eines Moduls verwendet werden.
Diese Methode parsed die zu übergebenden Werte, sowie die Rückgabewerte in den
korrekten Datentyp.

### func  CallValidate

```go
func CallValidate(functionName string, params ParameterMap) error
```
Wird zum Aufrufen der Validate-Methode eines Moduls verwendet werden. Diese
Methode parsed die zu übergebenden Werte, sowie die Rückgabewerte in den
korrekten Datentyp. Ist der zurückgegebene Error nil, sind alle Parameter
valide.

### func  GetModuleSyntax

```go
func GetModuleSyntax(module string) string
```
Sucht den Modul-Syntax für den Übergebenen Modul-Name oder Modul-Alias und gibt
diesen als formatierten String zurück.

### func  GetOS

```go
func GetOS() (string, error)
```
Versucht das Betriebssystem und seine Version zu bestimmen. Es wird nicht
zwischen den unterschiedlichen Ausführungen von einzelnen Windows-Versionen
(Home/Pro) etc. unterschieden.

### func  Initialize

```go
func Initialize(skipCompatibilityCheck bool) ([]ModuleSyntax, error)
```
Initialisiert alle Module und überprüft währenddessen, ob die Module mit dem
aktuellen OS kompatibel sind, und alle benötigten Methoden implementieren. Wenn
ja, wird der Syntax des Moduls ([ModuleSyntax](#type-modulesyntax)) in die Slice loadedModules
geschrieben. Mit `skipCompatibilityCheck` kann die Kompatibilitätsüberprüfung
übersprungen werden.

### func  ValidateAuditModules

```go
func ValidateAuditModules(mod []AuditModule) error
```
Überprüft für alle übergeben [AuditModule](#type-auditmodule)-Objekte ob das referenzierte
Modul eine Validate-Methode hat. Wenn ja, wird diese mit den in der
AuditKonfiguration angegebenen Parametern aufgerufen.

### func  callFunctionFromString

```go
func callFunctionFromString(function string, values []reflect.Value) []reflect.Value
```
Ruft die Methode mit dem übergebenen Name und den übergebenen Übergabewerten
auf. Gibt Rückgabewerte in einer Slice im Format reflect.Value zurück, die
zurück in den richtigen Datentyp gecasted werden muss.

### func  doesMethodExist

```go
func doesMethodExist(function string) bool
```
Überprüft ob eine Methode mit dem übergebenen Name in Sichtweite des
[MethodHandler](#type-methodhandler)-Objekts existiert.

### func  getModuleDescription

```go
func getModuleDescription(module ModuleSyntax) string
```
Formatiert den [ModuleSyntax](#type-modulesyntax) eines Moduls in einen string.

### func  hasDisallowedCharacters

```go
func hasDisallowedCharacters(in string) bool
```
True, wenn im übergebenen String für einen Modulname ungültige Zeichen enthalten
sind.

### func  parseParameterSliceToReflect

```go
func parseParameterSliceToReflect(in ParameterMap) []reflect.Value
```
Parsed eine [ParameterMap](#type-parametermap) in mit Reflect zu verwendenden Reflect-Values.

### func  parseReflectToError

```go
func parseReflectToError(in []reflect.Value) error
```
Parsed den Rückgabewert eines Calls in ein Error-Struct.

### func  parseReflectToModuleResult

```go
func parseReflectToModuleResult(in []reflect.Value) ModuleResult
```
Parsed den Rückgabewert eines Calls in ein [ModuleResult](#type-moduleresult)-Struct.

### func  parseReflectToModuleSyntax

```go
func parseReflectToModuleSyntax(in []reflect.Value) ModuleSyntax
```
Parsed den Rückgabewert eines Calls zurück in [ModuleSyntax](#type-modulesyntax).

### func  parseVariableMapToReflect

```go
func parseVariableMapToReflect(pm ParameterMap, vm *VariableMap) []reflect.Value
```
Parsed eine [ParameterMap](#type-parametermap), sowie [VariableMap](#type-variablemap) in mit Reflect zu
verwendenden Reflect-Values.

### func  sanityCheck

```go
func sanityCheck(mod []ModuleSyntax) error
```
Diese Methode überprüft, ob sich die in den Initialize-Methoden von Modulen
gesetzten Namen und Aliase überschneiden. Modulnamen müssen einzigarig sein. Ist
das nicht der Fall, wird ein passender Error geworfen.

### func  validateModule

```go
func validateModule(mod AuditModule) error
```
Überprüft ob das im [AuditModule](#type-auditmodule)-Objekt (also ein Audit-Schritt)
aufgerufene Modul die Validate-Methode implementiert. Wenn ja, wird sie mit den
gegebenen Parametern aufgerufen. Des Weiteren werden die Validate-Module von
Kindern des übergebenen Audit-Schritts ausgeführt. Sind alle Parameter laut den
Validate-Methoden valide wird nil zurückgegeben, ansonsten ein Error.

### func  wildcardCompatibilityCheck

```go
func wildcardCompatibilityCheck(moduleCompatibility []string) bool
```
Überprüft die Modul-Kompatibilität mit Wildcards gegeben ist
