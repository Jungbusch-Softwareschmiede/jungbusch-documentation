# modules

## Description

In diesem Package sind alle Module des Jungbusch-Auditoriums enthalten.

## Usage

### type MethodHandler

Mithilfe von diesem struct kann auf die Methoden der Module per Reflection
zugegriffen werden.


```go
type MethodHandler struct{}
```
### func (*MethodHandler) AuditPolicyQuery

```go
func (mh *MethodHandler) AuditPolicyQuery(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) AuditPolicyQueryInit

```go
func (mh *MethodHandler) AuditPolicyQueryInit() ModuleSyntax
```

### func (*MethodHandler) Auditctl

```go
func (mh *MethodHandler) Auditctl(params ParameterMap) (r ModuleResult)
```
Auditctl liefert die zurzeit geladenen Auditregeln

### func (*MethodHandler) AuditctlInit

```go
func (mh *MethodHandler) AuditctlInit() ModuleSyntax
```

### func (*MethodHandler) AuditctlValidate

```go
func (mh *MethodHandler) AuditctlValidate(params ParameterMap) error
```

### func (*MethodHandler) Authselect

```go
func (mh *MethodHandler) Authselect(params ParameterMap) (r ModuleResult)
```
ExecuteCommand führt den übergebenen Befehl aus und speichert das Ergebnis in
einem String.

### func (*MethodHandler) AuthselectInit

```go
func (mh *MethodHandler) AuthselectInit() ModuleSyntax
```

### func (*MethodHandler) AuthselectValidate

```go
func (mh *MethodHandler) AuthselectValidate(params ParameterMap) error
```

### func (*MethodHandler) AwkScript

```go
func (mh *MethodHandler) AwkScript(params ParameterMap) (r ModuleResult)
```
Awk ist eine Skriptsprache zum Editieren und Analysieren von Texten. AwkScript
führt ein Awk-Script, auf die Input-Datei aus

### func (*MethodHandler) AwkScriptInit

```go
func (mh *MethodHandler) AwkScriptInit() ModuleSyntax
```

### func (*MethodHandler) AwkScriptValidate

```go
func (mh *MethodHandler) AwkScriptValidate(params ParameterMap) error
```

### func (*MethodHandler) BashScript

```go
func (mh *MethodHandler) BashScript(params ParameterMap) (r ModuleResult)
```
ExecuteCommand führt den übergebenen Befehl aus und speichert das Ergebnis in
einem String.

### func (*MethodHandler) BashScriptInit

```go
func (mh *MethodHandler) BashScriptInit() ModuleSyntax
```

### func (*MethodHandler) CheckPartition

```go
func (mh *MethodHandler) CheckPartition(params ParameterMap) (r ModuleResult)
```
CheckPartition gibt alle eingehängten Datenträger aus. Ist der grep-Parameter
gesetzt, werden auch Zeilen zurückgegeben, in denen das Pattern gefunden wurde.

### func (*MethodHandler) CheckPartitionInit

```go
func (mh *MethodHandler) CheckPartitionInit() ModuleSyntax
```

### func (*MethodHandler) CheckPartitionValidate

```go
func (mh *MethodHandler) CheckPartitionValidate(params ParameterMap) error
```

### func (*MethodHandler) DumpSecuritySettings

```go
func (mh *MethodHandler) DumpSecuritySettings(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) DumpSecuritySettingsInit

```go
func (mh *MethodHandler) DumpSecuritySettingsInit() ModuleSyntax
```

### func (*MethodHandler) ExecuteCommand

```go
func (mh *MethodHandler) ExecuteCommand(params ParameterMap) (r ModuleResult)
```
ExecuteCommand führt den übergebenen Befehl aus und speichert das Ergebnis in
einem String.

### func (*MethodHandler) ExecuteCommandInit

```go
func (mh *MethodHandler) ExecuteCommandInit() ModuleSyntax
```

### func (*MethodHandler) ExecuteCommandValidate

```go
func (mh *MethodHandler) ExecuteCommandValidate(params ParameterMap) error
```

### func (*MethodHandler) ExportInstalledSoftware

```go
func (mh *MethodHandler) ExportInstalledSoftware(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) ExportInstalledSoftwareInit

```go
func (mh *MethodHandler) ExportInstalledSoftwareInit() ModuleSyntax
```

### func (*MethodHandler) FileContent

```go
func (mh *MethodHandler) FileContent(params ParameterMap) (r ModuleResult)
```
FileContent gibt den Inhalt der angegebenen Datei als String zurück. Ist der
grep-Parameter gesetzt, werden auch Zeilen zurückgegeben, in denen das Pattern
gefunden wurde.

### func (*MethodHandler) FileContentInit

```go
func (mh *MethodHandler) FileContentInit() ModuleSyntax
```

### func (*MethodHandler) FileContentValidate

```go
func (mh *MethodHandler) FileContentValidate(params ParameterMap) error
```

### func (*MethodHandler) GetAccountName

```go
func (mh *MethodHandler) GetAccountName(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) GetAccountNameInit

```go
func (mh *MethodHandler) GetAccountNameInit() ModuleSyntax
```

### func (*MethodHandler) GetAccountNameValidate

```go
func (mh *MethodHandler) GetAccountNameValidate(params ParameterMap) error
```

### func (*MethodHandler) GetUserSID

```go
func (mh *MethodHandler) GetUserSID(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) GetUserSIDInit

```go
func (mh *MethodHandler) GetUserSIDInit() ModuleSyntax
```

### func (*MethodHandler) GetWinEnv

```go
func (mh *MethodHandler) GetWinEnv(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) GetWinEnvInit

```go
func (mh *MethodHandler) GetWinEnvInit() ModuleSyntax
```

### func (*MethodHandler) Grep

```go
func (mh *MethodHandler) Grep(params ParameterMap) (r ModuleResult)
```
Grep liefert die Zeile, wo der Suchbegriff im Input übereinstimmt als String
zurück.

### func (*MethodHandler) GrepInit

```go
func (mh *MethodHandler) GrepInit() ModuleSyntax
```

### func (*MethodHandler) GrepValidate

```go
func (mh *MethodHandler) GrepValidate(params ParameterMap) error
```

### func (*MethodHandler) IsFile

```go
func (mh *MethodHandler) IsFile(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) IsFileInit

```go
func (mh *MethodHandler) IsFileInit() ModuleSyntax
```

### func (*MethodHandler) IsFileValidate

```go
func (mh *MethodHandler) IsFileValidate(params ParameterMap) error
```

### func (*MethodHandler) IsGPTemplatePresent

```go
func (mh *MethodHandler) IsGPTemplatePresent(params ParameterMap) (r ModuleResult)
```
Prüfen ob angegebene .admx/.adml File vorhanden ist

### func (*MethodHandler) IsGPTemplatePresentInit

```go
func (mh *MethodHandler) IsGPTemplatePresentInit() ModuleSyntax
```

### func (*MethodHandler) IsInstalled

```go
func (mh *MethodHandler) IsInstalled(params ParameterMap) (r ModuleResult)
```
IsInstalled liefert Informationen darüber, ob das angegeben Package installiert
ist.

### func (*MethodHandler) IsInstalledInit

```go
func (mh *MethodHandler) IsInstalledInit() ModuleSyntax
```

### func (*MethodHandler) IsInstalledValidate

```go
func (mh *MethodHandler) IsInstalledValidate(params ParameterMap) error
```

### func (*MethodHandler) IsNotInstalled

```go
func (mh *MethodHandler) IsNotInstalled(params ParameterMap) (r ModuleResult)
```
IsInstalled liefert Informationen darüber, ob das angegebene Package nicht
installiert ist.

### func (*MethodHandler) IsNotInstalledInit

```go
func (mh *MethodHandler) IsNotInstalledInit() ModuleSyntax
```

### func (*MethodHandler) IsNotInstalledValidate

```go
func (mh *MethodHandler) IsNotInstalledValidate(params ParameterMap) error
```

### func (*MethodHandler) Modprobe

```go
func (mh *MethodHandler) Modprobe(params ParameterMap) (r ModuleResult)
```
Modprobe simuliert das Laden des angegebenen Moduls zur Laufzeit des Systems und
speichert das Ergebnis ausführlich ab. Daraufhin wird überprüft, ob das
angegebene Modul aktuell geladen ist.

### func (*MethodHandler) ModprobeInit

```go
func (mh *MethodHandler) ModprobeInit() ModuleSyntax
```

### func (*MethodHandler) ModprobeValidate

```go
func (mh *MethodHandler) ModprobeValidate(params ParameterMap) error
```

### func (*MethodHandler) NftListRuleset

```go
func (mh *MethodHandler) NftListRuleset(params ParameterMap) (r ModuleResult)
```
NftListRuleset listet das Ruleset von nftables auf

### func (*MethodHandler) NftListRulesetInit

```go
func (mh *MethodHandler) NftListRulesetInit() ModuleSyntax
```

### func (*MethodHandler) NftListRulesetValidate

```go
func (mh *MethodHandler) NftListRulesetValidate(params ParameterMap) error
```

### func (*MethodHandler) Permissions

```go
func (mh *MethodHandler) Permissions(params ParameterMap) (r ModuleResult)
```
Permissions gibt Berechtigungen der/des übergebenden Datei/Ordners in
numerischer Form als String zurück.

### func (*MethodHandler) PermissionsInit

```go
func (mh *MethodHandler) PermissionsInit() ModuleSyntax
```

### func (*MethodHandler) PermissionsValidate

```go
func (mh *MethodHandler) PermissionsValidate(params ParameterMap) error
```

### func (*MethodHandler) RegistryQuery

```go
func (mh *MethodHandler) RegistryQuery(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) RegistryQueryInit

```go
func (mh *MethodHandler) RegistryQueryInit() ModuleSyntax
```

### func (*MethodHandler) Script

```go
func (mh *MethodHandler) Script(params ParameterMap, variables *VariableMap) (r ModuleResult)
```
Script führt JavaScript-Code aus um zum Beispiel auf andere Module zugreifen zu
können

### func (*MethodHandler) ScriptInit

```go
func (mh *MethodHandler) ScriptInit() ModuleSyntax
```

### func (*MethodHandler) ScriptValidate

```go
func (mh *MethodHandler) ScriptValidate(params ParameterMap) error
```

### func (*MethodHandler) SecuritySettingsQuery

```go
func (mh *MethodHandler) SecuritySettingsQuery(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) SecuritySettingsQueryInit

```go
func (mh *MethodHandler) SecuritySettingsQueryInit() ModuleSyntax
```

### func (*MethodHandler) Sshd

```go
func (mh *MethodHandler) Sshd(params ParameterMap) (r ModuleResult)
```
Sshd liest die Informationen aus der sshd Config-Datei aus

### func (*MethodHandler) SshdInit

```go
func (mh *MethodHandler) SshdInit() ModuleSyntax
```
TODO Update auf neue Benchmark

### func (*MethodHandler) SshdValidate

```go
func (mh *MethodHandler) SshdValidate(params ParameterMap) error
```

### func (*MethodHandler) Stat

```go
func (mh *MethodHandler) Stat(params ParameterMap) (r ModuleResult)
```
Mit dem Befehl Stat lassen sich Zugriffs- und Änderungs-Zeitstempel von Dateien
und Ordnern anzeigen. Weiterhin werden Informationen zu Rechten, zu Besitzer und
Gruppe und zum Dateityp ausgegeben.

### func (*MethodHandler) StatInit

```go
func (mh *MethodHandler) StatInit() ModuleSyntax
```

### func (*MethodHandler) StatValidate

```go
func (mh *MethodHandler) StatValidate(params ParameterMap) error
```

### func (*MethodHandler) Sysctl

```go
func (mh *MethodHandler) Sysctl(params ParameterMap) (r ModuleResult)
```
sysctl wird dazu verwendet, Kernelparameter zur Laufzeit zu ändern. Die
verfügbaren Parameter sind unter /proc/sys/ aufgelistet. Für die
sysctl-Unterstützung in Linux ist Procfs notwendig. Sie können sysctl sowohl zum
Lesen als auch zum Schreiben von Sysctl-Daten verwenden.

### func (*MethodHandler) SysctlInit

```go
func (mh *MethodHandler) SysctlInit() ModuleSyntax
```

### func (*MethodHandler) SysctlValidate

```go
func (mh *MethodHandler) SysctlValidate(params ParameterMap) error
```

### func (*MethodHandler) Systemctl

```go
func (mh *MethodHandler) Systemctl(params ParameterMap) (r ModuleResult)
```
Systemctl überprüft, ob die angegebene Unitdatei aktiviert ist.

### func (*MethodHandler) SystemctlInit

```go
func (mh *MethodHandler) SystemctlInit() ModuleSyntax
```

### func (*MethodHandler) SystemctlValidate

```go
func (mh *MethodHandler) SystemctlValidate(params ParameterMap) error
```

### func (*MethodHandler) Template

```go
func (mh *MethodHandler) Template(params ParameterMap) (r ModuleResult)
```

### func (*MethodHandler) TemplateInit

```go
func (mh *MethodHandler) TemplateInit() ModuleSyntax
```

### func (*MethodHandler) TemplateValidate

```go
func (mh *MethodHandler) TemplateValidate(params ParameterMap) error
```

### func  exportVariables

```go
func exportVariables(vm *goja.Runtime, variables VariableMap) *VariableMap
```

### func  initLogging

```go
func initLogging(vm *goja.Runtime) (err error)
```

### func  initModules

```go
func initModules(vm *goja.Runtime, mh *MethodHandler) (err error)
```
Initialisiert den MethodHandler in JS mit allen Modulen

### func  initVariables

```go
func initVariables(vm *goja.Runtime, variables VariableMap) (err error)
```

### func  newResult

```go
func newResult(result, resultRaw string, err error) ModuleResult
```
