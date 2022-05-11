---
layout: default
title: Excel VBA
parent: Microsoft 365
---

# Excel VBA

## Procedures

There are three kinds of procedures: `sub`, `function`, and `property` procedures. A function must return a value, while a sub can't.

### ByVal and ByRef

Generally, it is best to use `ByVal` for parameters. Use `ByRef` only when it is necessary to reassign the parameter for the caller as well. Always specify since `ByRef` is used by VBA as default.

## Explicicity

### Option explicit
Adding `Option explicit` to the top of the file will force the use of `Dim X As Y` instead of `Dim X` which will implicitly use the `Variant` data type.

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

```vb
Dim ReadRange As Range
Set ReadRange = Sheet.Cells(2, 1).Resize(NumRows, NumCols)
Dim Values() As Variant
Values = ReadRange.Value2
Dim Row As Long
For Row = LBound(Values, 1) To UBound(Values, 1)
    <...>
Next Row
```

The same goes for writing to multiple cells.

```vb
Dim WriteRange As Range
Set WriteRange = MainSheet.Cells(6, 2).Resize(NumRows, NumCols)
WriteRange.Value2 = Values
```

### Disable Excel functionality while your code is running

As written in [Excel VBA Performance Coding Best Practices by Diego Oppenheimer](https://www.microsoft.com/en-us/microsoft-365/blog/2009/03/12/excel-vba-performance-coding-best-practices/).

### Don't select

There is no need. `Select` and `Selection` is slower and not as readable. Use `Activate` if you would like to show a specific worksheet to the user.

## Error Handling

It's possible to use the error handler to return to the code after an error is handled. When a runtime error occurs, VBA automatically fills the `Err` object with details such as `Err.Description` and `Err.Number`. You can raise errors manually with `Err.Raise`. Similarly to `Throw` in Java and C#.

```vb
On Error GoTo 0       ' Default behavior. The code stops at the line with
                      ' the error and displays a message.
                      
On Error Resume Next  ' Ignore. The code moves to the next line and no error
                      ' message is displayed. This should usually be avoided.
                      
On Error GoTo [label] ' How error handling is used in VBA. The code moves to
                      ' a specific line or label. No error message is displayed.
                      ' The label must be in the burrent Sub/Function.
                      
On Error GoTo -1      ' Clears the current error. Necessary with multiple error
                      ' handlers.
```

 Read more at [VBA Error Handling (ExcelMacroMastery)](https://excelmacromastery.com/vba-error-handling/).

## Syntax examples

### Array

```vb
Dim Values() As Variant
ReDim Values(1 To NumRows, 1 To NumCols) As Variant

For Row = LBound(Values, 1) To UBound(Values, 1)
    <...>
Next Row
```

### If Then Else Statement

```vb
If foo = 2 Then
    bar = "Yes"
ElseIf foo = 1 Then
    bar = "Maybe"
Else
    bar = "No"
End If
```

### For Loops

```vb
' For Next Loop
Dim RowNr As Integer
For RowNr = 1 to 10
    If Cells(RowNr, 1).Value <> "" Then
        Exit For ' Breaks out of the loop entirely
    End If
    Cells(RowNr, 1).Value = "foo"
Next RowNr ' Increments and iterates

' For Each Next Loop
Dim CurrentSheet As Worksheet
For Each CurrentSheet In ThisWorkbook.Worksheets
    MsgBox "Found worksheet: " & CurrentSheet.Name
Next CurrentSheet
```

### Do Loops

```vb
' Do While Loop
Dim RowNr As Integer
RowNr = 5

Do While Cells(RowNr, 1).Value <> "" ' Not empty
    Cells(RowNr, 3).Value = Cells(RowNr, 2) + 30
    RowNr = RowNr + 1
Loop
```

### Select Case Statement

```vb
Select Case Foo
    Case 0
        MsgBox "Foo is 0"
    Case 1
        MsgBox "Foo is 1"
    Case Else
        MsgBox "Foo is something else"
End Select
```

### With Statement

```vb
With CellRange.Font
    .Name = "Arial"
    .Size = 14
    .Bold = True
End With
```