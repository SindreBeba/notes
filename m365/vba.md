---
layout: default
title: Excel VBA
parent: Microsoft 365
---

# Excel VBA

## Procedures

There are three kinds of procedures: `sub`, `function`, and `property` procedures. A function must return a value, while a sub can't.

### `ByVal` and `ByRef`

Generally, it is best to use `ByVal` for parameters. Use `ByRef` only when it is necessary to reassign the parameter for the caller as well. Always specify since `ByRef` is used by VBA as default.

## Explicicity

### Application

The `Application` object can change during runtime if the user opens another Excel workbook. Because of this, it is a good idea to be explicit in calls that involve `Application`.

`ThisWorkbook.Worksheets` instead of simply `Worksheets` which is an implicit call to `Application.Activebook.Worksheets`.

### Object instantiation

Explicitly instantiate a new object with `Dim Foo As Bar: Set Foo = New Bar` instead of using the shorter syntax `Dim Foo As New Bar`. Using the latter, the object will not be instantiated before the first time it is referenced.

## Best practices

### Prefer compile errors to runtime errors

As an example, write `Sheet Is MainSheet` instead of `Sheet.CodeName = "MainSheet"`.

### Read and write to cells in bulks

It is far more effective to read and write to cells in batches. Instead of iterating over each row and column while using `Cells(RowNr, ColNr)`, it is better to read all the values using `Range` and the iterate over the array.

```vba
Dim ReadRange As Range
Set ReadRange = Sheet.Cells(2, 1).Resize(NumRows, NumCols)
Dim Values() As Variant
Values = ReadRange.Value2
Dim Row As Long
For Row = LBound(Values, 1) To UBound(Values, 1)
    ...
Next Row
```

The same goes for writing to multiple cells.

```vba
Dim WriteRange As Range
Set WriteRange = MainSheet.Cells(6, 2).Resize(NumRows, NumCols)
WriteRange.Value2 = Values
```