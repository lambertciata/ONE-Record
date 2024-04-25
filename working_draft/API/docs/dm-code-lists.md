ONE Record data model 3.0 introduced code lists for type safety. These replaced data properties holding enumberations and strings referencing a particular code list.
Code lists are built on using custom objects. Many code lists are published as named individuals in the [ONE Record coreCodeLists ontology] (https://onerecord.iata.org/ns/coreCodeLists).
For unpublished or open code lists, the embedded object [CodeListElement](https://onerecord.iata.org/ns/cargo#CodeListElement) is used. A code list is open when it is not exhaustive.
The approach also allows to refer codes defined as linked data outside of ONE Record. This includes, for example, code lists published as part of the [BSP data model of UN/CEFACT](https://vocabulary.uncefact.org/code-lists).
This page provides guidance on how to use code lists in practical use cases.

# CodeListElement

The `CodeListElement` is an embedded object. It is the superclass of all other code lists in ONE Record.
As such, all codes defined as named individuals are viewed as instances of the `CodeListElement`.
It features the following properties if a custom instance as embedded object is required:

| Property| Description               |
| ------- |  ----------------------- |
| code | Code or short version of a code, for example "CH" for Switzerland when referring to the UN/LOCODE code list |
| codeDescription | Description or long version of the code, for example "Switzerland" for Switzerland when referring to the UN/LOCODE code list |
| codeLevel | Integer indicating the level of a code if a code list is hierarchical, for example HS-Codes |
| codeListName| Official name of the code list without version number when direct reference is not possible, for example "UN/LOCODE" when referring to the UN/LOCODE code list |
| codeListReference | 	URL to access the code list the code is taken from, for example "https://unece.org/trade/cefact/unlocode-code-list-country-and-territory" for UN/LOCODE. |
| codeListVersion | Version of the code list, for example "223-1" for UN/LOCODE. Used if the property codeListName is used or the version is not apparent from the resource referred to in property codeListReference. |

!!! note
    The properties [code](https://onerecord.iata.org/ns/cargo#code) and either [codeListName](https://onerecord.iata.org/ns/cargo#codeListName) or [codeListReference](https://onerecord.iata.org/ns/cargo#codeListReference) at least "SHOULD" be used if instanced.

# Examples

## Using a named individual for an enumberation

## Using a code from a closed code list defined in ONE Record

## Using a defined code from an open code list defined in ONE Record

## Using an undefined code from an open code list defined in ONE Record

## Using an undefined code that is not published as linked data

## Using a defined code defined by another linked data vocabulary
