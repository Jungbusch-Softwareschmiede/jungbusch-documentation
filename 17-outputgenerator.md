# outputgenerator

## Description

## Usage

### type Metadata



```go
type Metadata struct {
	Os           string        `json:"os"`
	Root         bool          `json:"root"`
	Total        int           `json:"total"`
	Passed       int           `json:"passed"`
	Notpassed    int           `json:"not_passed"`
	Unsuccessful int           `json:"unsuccessful"`
	Notexecuted  int           `json:"not_executed"`
	Started      string        `json:"started"`
	Elapsed      string        `json:"elapsed"`
	Report       []ReportEntry `json:"report"`
}
```
### type ReportEntry



```go
type ReportEntry struct {
	ID        string            `json:"id"`
	Desc      string            `json:"desc"`
	Print     string            `json:"print,omitempty"`
	Artifacts []models.Artifact `json:"artifacts"`
	Expected  string            `json:"expected,omitempty"`
	Actual    string            `json:"actual,omitempty"`
	Error     string            `json:"error,omitempty"`
	Result    string            `json:"result"`
	Nested    []ReportEntry     `json:"nested,omitempty"`
}
```
### func  cleanArtifacts

```go
func cleanArtifacts(report []ReportEntry) []ReportEntry
```

### type stats



```go
type stats struct {
	total        int
	passed       int
	notpassed    int
	unsuccessful int
	notexecuted  int
}
```
### func  getStats

```go
func getStats(report []ReportEntry, numberOfModules int) (s stats)
```

### func  GenerateOutput

```go
func GenerateOutput(report []ReportEntry, outputPath string, numberOfModules int, zip bool, start time.Time, elapsed time.Duration) error
```
GenerateOutput erstellt den Report und speichert die Artefakte am spezifizierten
Pfad.

### func  generateReport

```go
func generateReport(report []ReportEntry, outputPath string, numberOfModules int, start time.Time, elapsed time.Duration) (err error)
```

### func  saveArtifacts

```go
func saveArtifacts(report []ReportEntry, outputPath string) error
```

### func  zipFolder

```go
func zipFolder(folder string) error
```
