# SonarQube

## Disabling SonarQube analysis

```c++
const char* table[] = {
    "entry1", //NOSONAR
    "entry2", //NOSONAR
    "entry3"  //NOSONAR
};
```

```c++
//NOSONAR:cpp:S1186  Reason for duplication: Performance optimization in this specific case.
int duplicatedFunction() {
  // ... identical code ...
}
```

```c++
// SONAR:OFF
static const table[] = {
  {1, "Value1"},
  {2, "Value2"},
  {3, "Value3"}
};
// SONAR:ON
```

```c++
// BEGIN-NOSCAN
public void doSomethingElse()
{
    ...
}
// END-NOSCAN
```

See also <https://docs.sonarsource.com/sonarqube-server/2025.1/project-administration/analysis-scope#ignoring-blocks-within-files>

## How coverage is calculated

### Coverage

Coverage is a combination of lines to cover and conditions to cover:

```text
coverage = (CT + LC) / (B + EL)
```

where:

* `CT`: conditions that have been evaluated to true at least once = `conditions_to_cover - uncovered_conditions`
* `LC`: `covered lines = lines_to_cover - uncovered_lines`
* `B`: total number of conditions = Conditions to Cover
* `EL`: total number of executable lines (`lines_to_cover`)

See also <https://docs.sonarsource.com/sonarqube-server/user-guide/code-metrics/metrics-definition#coverage>.

### Line Coverage

Line coverage is the density of covered lines by unit tests:

```text
line_coverage = LC / EL
```

where:

* `LC` = covered lines = `lines_to_cover - uncovered_lines`
* `EL` = total number of executable lines (`lines_to_cover`)

### Condition Coverage

TODO

## Debugging sonar-scanner

The following options are useful for debugging:

```text
-Dsonar.log.level=TRACE (or DEBUG)
-Dsonar.verbose=true
```
