<div align="center">

## Window\.\.\. Windows Logo


</div>

### Description

You can make you form just like a Window.. in fact just like microsoft windows, window... :)
 
### More Info
 
You need to add a timer to the form thats it...


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Fatal3rr0r](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/fatal3rr0r.md)
**Level**          |Intermediate
**User Rating**    |3.8 (15 globes from 4 users)
**Compatibility**  |VB 3\.0, VB 4\.0 \(16\-bit\), VB 4\.0 \(32\-bit\), VB 5\.0, VB 6\.0
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__1-1.md)
**World**          |[Visual Basic](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/visual-basic.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/fatal3rr0r-window-windows-logo__1-7508/archive/master.zip)





### Source Code

```
Option Explicit
Private Type RECT
    Left As Long
    Top As Long
    Right As Long
    Bottom As Long
End Type
Private Declare Function BeginPath Lib "gdi32" (ByVal hdc As Long) As Long
Private Declare Function TextOut Lib "gdi32" Alias "TextOutA" (ByVal hdc As Long, _
    ByVal X As Long, ByVal Y As Long, _
    ByVal lpString As String, _
    ByVal nCount As Long) As Long
Private Declare Function EndPath Lib "gdi32" (ByVal hdc As Long) As Long
Private Declare Function PathToRegion Lib "gdi32" (ByVal hdc As Long) As Long
Private Declare Function GetRgnBox Lib "gdi32" (ByVal hRgn As Long, lpRect As RECT) _
    As Long
Private Declare Function CreateRectRgnIndirect Lib "gdi32" (lpRect As RECT) As Long
Private Declare Function CombineRgn Lib "gdi32" (ByVal hDestRgn As Long, _
    ByVal hSrcRgn1 As Long, _
    ByVal hSrcRgn2 As Long, _
    ByVal nCombineMode As Long) As Long
Private Const RGN_AND = 1
Private Declare Function DeleteObject Lib "gdi32" (ByVal hObject As Long) As Long
Private Declare Function SetWindowRgn Lib "user32" _
    (ByVal hwnd As Long, ByVal hRgn As Long, _
    ByVal bRedraw As Boolean) As Long
Private Declare Function ReleaseCapture Lib "user32" () As Long
Private Declare Function SendMessage Lib "user32" Alias "SendMessageA"  _
    (ByVal hwnd As Long, _
    ByVal wMsg As Long, ByVal wParam As Long, _
    lParam As Any) As Long
Private Const WM_NCLBUTTONDOWN = &HA1
Private Const HTCAPTION = 2
Private Function GetTextRgn() As Long
    Dim hRgn1 As Long, hRgn2 As Long
    Dim rct As RECT
    BeginPath hdc
    TextOut hdc, 10, 10, Chr$(255), 1
    EndPath hdc
    hRgn1 = PathToRegion(hdc)
    GetRgnBox hRgn1, rct
    hRgn2 = CreateRectRgnIndirect(rct)
    CombineRgn hRgn2, hRgn2, hRgn1, RGN_AND
    'Return the region handle
    DeleteObject hRgn1
    GetTextRgn = hRgn2
End Function
Private Sub Form_DblClick()
    Unload Me
End Sub
Private Sub Form_Load()
    Dim hRgn As Long
    Me.Font.Name = "Wingdings"
    Me.Font.Size = 200
    hRgn = GetTextRgn()
    MsgBox "Remember, Double Click on Flag to Close Me", vbInformation
    SetWindowRgn hwnd, hRgn, 1
End Sub
Private Sub Form_MouseDown(Button As Integer, Shift As Integer, X As Single, Y As Single)
    ReleaseCapture
    SendMessage hwnd, WM_NCLBUTTONDOWN, HTCAPTION, ByVal 0&
End Sub
Private Sub Timer1_Timer()
    Me.BackColor = RGB(Rnd * 255, Rnd * 255, Rnd * 255)
End Sub
```

