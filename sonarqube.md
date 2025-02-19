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
