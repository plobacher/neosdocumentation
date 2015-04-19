# TypoScript: Best pratices


* [Eel](../eel/README.md) (Embedded Expression Language)
* [FlowQuery](../flowquery/README.md)

## Ermittelt der Array-Keys von documentNode.properties
```
${Array.join(Array.keys(documentNode.properties))}
```