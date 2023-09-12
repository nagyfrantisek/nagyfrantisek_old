---
title: "Separate charts for each row in Excel"
layout: post
date: 2023-09-12 22:10
tags: excel
categories: blog
description: separate charts for each row
---

VBA script:
```
Sub DuplicateActiveChartOncePerRow()
  If ActiveChart Is Nothing Then
    MsgBox "Select a chart and try again!", vbExclamation + vbOKOnly
    GoTo ExitSub
  End If
  Dim nCharts As Long
  nCharts = ActiveSheet.ChartObjects.Count
  Dim OriginalChart As Chart
  Set OriginalChart = ActiveChart
  
  ' SERIES formula
  Dim sFormula As String
  sFormula = OriginalChart.SeriesCollection(1).Formula
  ' formula arguments only
  sFormula = Mid$(Left$(sFormula, Len(sFormula) - 1), InStr(sFormula, "(") + 1)
  ' array of arguments
  Dim vFormula As Variant
  vFormula = Split(sFormula, ",")
  
  ' series name - first argument
  Dim sName As String
  sName = vFormula(LBound(vFormula))
  Dim rName As Range
  On Error Resume Next
  Set rName = Range(sName)
  On Error GoTo 0
  Dim bNameIsRange As Boolean
  bNameIsRange = Not rName Is Nothing
  
  ' y values - third argument
  Dim sYVals As String
  sYVals = vFormula(LBound(vFormula) + 2)
  Dim rYVals As Range
  On Error Resume Next
  Set rYVals = Range(sYVals)
  On Error GoTo 0
  If rYVals Is Nothing Then
    MsgBox "Y Values Are Not in a Range!", vbExclamation + vbOKOnly
    GoTo ExitSub
  End If
  
  Dim iChart As Long
  iChart = 1
  Do
    ' loop until we run out of Y values
    If WorksheetFunction.Count(rYVals.Offset(iChart)) = 0 Then
      MsgBox "Finished!", vbExclamation + vbOKOnly
      GoTo ExitSub
    End If
    ' make copy of original chart
    OriginalChart.Parent.Copy
    Do
      ' loop to avoid error because sometimes clipboard isn't ready to paste
      DoEvents
      On Error Resume Next
      ActiveSheet.Paste
      On Error GoTo 0
      If ActiveSheet.ChartObjects.Count >= nCharts + iChart Then Exit Do
    Loop
    Dim NewChart As Chart
    Set NewChart = ActiveSheet.ChartObjects(ActiveSheet.ChartObjects.Count).Chart
    NewChart.Parent.Left = OriginalChart.Parent.Left
    NewChart.Parent.Top = OriginalChart.Parent.Top + iChart * rYVals.Height
    ' change Y values and name in new chart
    With NewChart.SeriesCollection(1)
      .Values = rYVals.Offset(iChart)
      If bNameIsRange Then
        .Name = "=" & rName.Offset(iChart).Address(, , , True)
      End If
    End With
    iChart = iChart + 1
  Loop
  
ExitSub:
End Sub
```