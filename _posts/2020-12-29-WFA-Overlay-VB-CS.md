---
title: Simple WFA Overlay
layout: post
description: Making a simple WFA overlay in vs.net and c#.net (for games)
tags: post c# vb .NET overlay tutorial
minute: 6
---

## Introduction
Have you ever wondered how to make a form, that always stays in front of a window, while being completely click through and having a transparent background?
Two months ago, I wanted to create a form that overlays the popular game Among Us in c#.net. In this short tutorial I want to explain to you how you can exactly the explained behavior in c# and Visual Basic!
#### Creating a new project
These first steps are the same for c#.net and vb.net.
* Start out by opening Visual Studio
* Click on "Create a new project"
* In the section "Get Started" choose "Create a new project"
* Press Alt + S and search for "Windows Forms App (.NET FRAMEWORK)" and choose either the C# or Visual Basic example
* Name the project whatever you want and click "Create" in the bottom right

#### Adjusting properties in the Designer
In the bottom right you will see a section called Properties
* Set the "[BackColor](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.form.backcolor?view=netframework-4.8)" and "[TransparencyKey](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.form.transparencykey?view=netframework-4.8)" to some color you don't like or need. I'm choosing "Olive" from the "Web" tab
* Change "[FormBorderStyle](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.form.formborderstyle?view=netframework-4.8)" to "None"
* Set "[TopMost](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.form.topmost?view=netframework-4.8)" to "True"
* (optional) if you later experience any kind of flickering set "[DoubleBuffered](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.control.doublebuffered?view=netframework-4.8)" to "true"
* From the Toolbox(located on the left) drag a timer onto your form
* Change the "[Enaled](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.timer.enabled?view=netframework-4.8)" property of the timer from "False" to "True" and the "[Interval](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.timer.interval?view=netframework-4.8)" from "100"(ms) to "10"(ms)
* Double-click your Form and switch back to the tab with [Design] in the title
* Now double-click the timer and continue in the next section

#### The Code
1) First we need to import a few functions from user32.dll, but to enable DLL import, we first need to import [InteropServices](https://docs.microsoft.com/en-us/previous-versions/windows/apps/9esea608(v=vs.105)?f1url=%3FappId%3DDev16IDEF1%26l%3DEN-US%26k%3Dk(System.Runtime.InteropServices))

(Visual Basic) Just add this as the first line of your file
``` vb
Imports System.Runtime.InteropServices
```
(C#) Add this line after all other "using" statements 
``` csharp
using System.Runtime.InteropServices
```
Then import "[GetWindowLong](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getwindowlonga)", "[SetWindowLong](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-setwindowlonga)", "[FindWindow](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-findwindowa)" and "[GetWindowRect](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getwindowrect)"

"GetWindowLong" and "SetWindowLong" are needed to get and set the current  window style to make it clickthrough.

"FindWindow" is needed to retrieve a [handle](https://docs.microsoft.com/en-us/dotnet/api/system.intptr?view=netframework-4.8&f1url=%3FappId%3DDev16IDEF1%26l%3DEN-US%26k%3Dk(System.IntPtr)) of the top most window with a specific window name (a window's title).

"GetWindowRect" is needed to get the Rectangle a window is located in by the handle we retrieve via "FindWindow".

(Visual Basic) Add this code after "Public Class Form1":
``` vb
<DllImport("user32.dll")> Public Shared Function GetWindowLong(ByVal hWnd As IntPtr, ByVal nIndex As Integer) As Integer
End Function

<DllImport("user32.dll")> Public Shared Function SetWindowLong(ByVal hWnd As IntPtr, ByVal nIndex As Integer, ByVal dwNewLong As Integer) As Integer
End Function

<DllImport("user32.dll")> Public Shared Function FindWindow(ByVal lpClassName As IntPtr, ByVal lpWindowName As String) As IntPtr
End Function

<DllImport("user32.dll")> Private Shared Function GetWindowRect(ByVal hWnd As IntPtr, ByRef lpRect As RECT) As Boolean
End Function
```

(C#) Add this code after "public partial class Form1 : Form":
``` csharp
[DllImport("user32.dll")]
static extern int SetWindowLong(IntPtr hWnd, int nIndex, int dwNewLong);

[DllImport("user32.dll")]
static extern int GetWindowLong(IntPtr hWnd, int nIndex);

[DllImport("user32.dll")]
static extern IntPtr FindWindow(string lpClassName, string lpWindowName);

[DllImport("user32.dll")]
static extern bool GetWindowRect(IntPtr hWnd, out RECT lpRect);
```
2) To make the form click through we first need to retrieve the [extended window styles](https://docs.microsoft.com/en-us/windows/win32/winmsg/extended-window-styles) of our current form with "GetWindowLong". After that we can modify these values with "SetWindowLong".

(Visual Basic) Put this code right before the DLLImports from section 1)
``` vb
Private InitialStyle As Integer
```
(Visual Basic) Put this code in the automatically created "Form1_Load" sub procedure:
``` vb
InitialStyle = GetWindowLong(Me.Handle, -20)
SetWindowLong(Me.Handle, -20, InitialStyle Or &H80000 Or &H20)
```

(C#) Put this code in the {}brackets of the automatically created "Form1_Load" function:
``` csharp
int initialStyle = GetWindowLong(this.Handle, -20);
SetWindowLong(this.Handle, -20, initialStyle | 0x80000 | 0x20);
```
* -20 / GWL_EXSTYLE signals GetWindowLong and SetWindowLong to specifically use [extended window styles](https://docs.microsoft.com/en-us/windows/win32/winmsg/extended-window-styles)
* 0x80000 / WS_EX_LAYERED creates a [layered window](https://docs.microsoft.com/en-us/windows/win32/winmsg/window-features?redirectedfrom=MSDN#layered-windows)
* 0x20 / WS_EX_TRANSPARENT makes the window transparent to hit-tests.

3) In order to move the window, we use the previously created timer to update the form position according to the position of the targeted window. We first have to define the name of the target window to then get a window handle. Please replace "This PC" with the Name of your target window.

(Visual Basic) We best place this code after our DLLImports from step 1)
``` vb
Public Const WINDOW_NAME As String = "This PC"
Dim h = FindWindow(Nothing, WINDOW_NAME)
```

(C#) We best place this code after our DLLImports from step 1)
``` csharp
public const string WINDOW_NAME = "This PC";
IntPtr handle = FindWindow(null, WINDOW_NAME);
```

4) Then we need to define a rectangle, where we can later put the attributes of our target window, which we will later apply to our own window.

(Visual Basic) Place this code directly after the last code segment
``` vb
<StructLayout(LayoutKind.Sequential)> Public Structure RECT
    Dim Left, Top, Right, Bottom As Integer
End Structure

Dim r As RECT
```

(C#) Place this code directly after the last code segment
``` csharp
public struct RECT
{
    public int left, top, right, bottom;
}

RECT rect;
```

5) For every tick (every 10 ms or so, depending on if you have changed the interval) of the timer we can now get the rectangle of the target window and apply the dimensions to our own window.

(Visual Basic) Put this code in the automatically created "Timer1_Tick" sub procedure:
``` vb
GetWindowRect(h, r)
Me.Size = New Size(r.Right - r.Left, r.Bottom - r.Top)
Me.Top = r.Top
Me.Left = r.Left
```

(C#) Put this code in the {}brackets of the automatically created "Timer1_Tick" function:
``` csharp
GetWindowRect(handle, out rect);
this.Size = new Size(rect.right - rect.left, rect.bottom - rect.top);
this.Top = rect.top;
this.Left = rect.left;
```

#### Custom Elements
You have finished the main part of the tutorial (Congrats 🎉). You can now add custom elements to your form to test if your overlay works. Go back to the tab with [Design] in the name and drag a Label from the Toolbox onto the Form and change the "[BackColor](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.control.backcolor?view=netframework-4.8)" to "Control" or something similar and press the "Start" Button at the top of the window, but make sure that you have opened your target window first, else it obviously won't work :)