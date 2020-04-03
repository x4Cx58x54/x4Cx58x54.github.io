---
title: 网络计划图绘制总结
---

# 网络计划图绘制总结 | Network Planning Review

## VB.net

### Code

#### Comments
```vb
'Comments
```
Multi-line comments: `Ctrl+K+C`  
Cancel multiline comments: `Ctrl+K+U`

#### Array
```vb
Dim <array_name>(<size>) As <type>
```

#### Select Case
```vb
Select Case <variable_name>
    Case <value>
        <statements>
    Case <value>
        <statements>
    Case Else
        <statements>
End Select
```

#### Try-Catch
```vb
Try
    <statements>
Catch
    <statements>
Finally
    <statements>
End Try
```
Execute try statements first. Go to catch statements on  exception, and finally execute finally statements anyway.

#### Throw Exception
```vb
Throw New Exception
```

#### Declarations and Definitions
```vb
'local variables
Dim <variable_name> As <type> [= <default_value>]

'sub
Public Sub <sub_name>(<parameter_list>)
    <statements>
    [Return]
End Sub

'function
Public Function <function_name>(<parameter_list>) As <type>
    <statements>
    Return <value>
End Function

'parameter list
[ByVal] <parameter_name> As <type>[, ...]
ByRef <parameter_name> As <type>
Optional <parameter_name> As <type> = <value>
```

`ByVal` transfer by value  
`ByRef` transfer by reference  

#### Global Declarations
```vb
Module <module_name>
    Public <variable_name> As <type> [= <default_value>]
End Module
```

#### Load Form / Dialog and Non-dialog
```vb
Dim <obj_name> As New <form_name>
<obj_name>.Show()       'Non-dialog mode
<obj_name>.ShowDialog() 'Dialog mode, will disable parent form temporarily.
```

#### Close / Dispose Form
```vb
Dispose()   'Destroy form
Close()     'Close form
```

#### Msgbox (Message Box)
[MsgBox - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/microsoft.visualbasic.interaction.msgbox?view=netframework-4.7.2#Microsoft_VisualBasic_Interaction_MsgBox_System_Object_Microsoft_VisualBasic_MsgBoxStyle_System_Object_)
```vb
MsgBox(<content>, <style>, <title>)

'style
MsgBoxStyle.<style_name>
```

#### String
```vb
<string> + <string>
Trim(<string>)                              'Sub, remove beginning and ending spaces
LTrim(<string>)
RTrim(<string>)
<string>.Replace(<old_str>, <new_str>)      'Returns a string
Str(<number>)                               'Returns a string, convert number to string
Val(<string>)                               'Convert string to number 
<string>.Substring(<start_loc>, <length>)   'Returns a string
<string>.Contains(<pattern>)                'Returns a boolean
Split(<string>, <separator_string>)         'Returns a string array starting from (0)
IsNumeric(<string>)
Asc(<char>)                                 'Returns the ASCII code

```

#### Spcial Characters
```vb
vbTab   'Tab
vbCrLf  'Line return
```

#### Colour
[Color Enum - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.drawing.color?view=netframework-4.7.2)
```vb
Imports System.Drawing
...

<colour_attribute>=Color.<color_name>
```

#### Paths
```vb
Application.StartupPath
```

#### URL
```vb
<url_attribute>=New Uri(<url_as_string>)
```

#### File Operations
```vb
IO.File.Exists(<file_path>)
IO.File.Delete(<file_path>)
IO.Directory.Exists(<dir_path>)
IO.Directory.Delete(<dir_path>)
IO.Directory.CreateDirectory(<dir_path>)
```

#### StreamReader | 流读取文件
[StreamReader - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.io.streamreader?view=netframework-4.7.2)
```vb
Dim <reader_name> As New StreamReader(<file_path>, <encoding>)      'Encoding default UTF-8
<reader_name>.Read()        'Returns a character
<reader_name>.ReadLine()    'Returns a string
<reader_name>.Peek()        'Returns a character
<reader_name>.Close()
```

#### StreamWriter | 流写入文件
[StreamWriter - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.io.streamwriter?view=netframework-4.7.2)
```vb
Dim <writer_name> As New StreamWriter(<file_path>, <append>, <encoding>)    '<append> true to append data, false to overwrite
<writer_name>.Write(<string>)
<writer_name>.Close()
```

#### Encoding | 字符编码
[Encoding - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.text.encoding?view=netframework-4.7.2)
```vb
Imports System.Text
...

Encoding.UTF8
Encoding.ASCII
```

#### OpenFileDialog | 打开文件对话框
[OpenFileDialog - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.openfiledialog?view=netframework-4.7.2)
```vb
Imports System.Windows.Forms
...

Dim <dialog_name> As New OpenFileDialog
<dialog_name>.InitialDirectory = <dir_path>
<dialog_name>.Filter = <filter_string>          'eg. "Text files (*.txt)|*.txt"
<dialog_name>.FilterIndex = <integer>           
<dialog_name>.RestoreDirectory = <boolean>

openFileDialog.ShowDialog()             'Function, opens the dialog and returns dialog result
openFileDialog.FileName()               'File name
```

#### SaveFileDialog | 保存文件对话框
[SaveFileDialog - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.savefiledialog?view=netframework-4.7.2)
```vb
Imports System.Windows.Forms
... 

Dim <dialog_name> As New SaveFileDialog
<dialog_name>.Title = <string>
<dialog_name>.InitialDirectory = <dir_path>
<dialog_name>.Filter = <filter_string>
<dialog_name>.FilterIndex = <integer>
<dialog_name>.RestoreDirectory = <boolean>
<dialog_name>.FileName = <file_path>

<dialog_name>.ShowDialog()             'Function, saves the file and returns dialog result
```

#### DialogResult
[DialogResult - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.windows.forms.dialogresult?view=netframework-4.7.2)
```vb
Imports System.Windows.Forms
... 

DialogResult.OK
DialogResult.Cancel
DialogResult.Yes
DialogResult.No
```

#### Mutex (Mutal Exclusion) | 互斥锁
[Mutex - Microsoft Documentation](https://docs.microsoft.com/en-us/dotnet/api/system.threading.mutex?view=netframework-4.7.2)
```vb
Imports System.Threading        'Mutex class
Imports System.Windows.Forms    'Application class

Sub main()
        Dim onlyInstance As Boolean = False
        Dim Mutex = New Mutex(True, "UniqueApplicationName", onlyInstance)
        If onlyInstance = False Then
            <MsgBox>
            Return
        End If
        Application.Run(New <MainForm_name>)
        GC.KeepAlive(Mutex)
    End Sub
```

#### Excel Operations
```vb
Imports Microsoft.Office.Interop

...

Dim xlfilename As String                                                 'read and write excel(.xlsx) files
xlfilename = <file_name>
If System.IO.Directory.Exists(xlfilename) = False Then File.Delete(xlfilename)
Dim xlapp As Excel.Application                                           'Excel object
Dim xlbook As Excel.Workbook 
Dim xlsheet As Excel.Worksheet

xlapp = CreateObject("Excel.Application")
xlbook = xlapp.Workbooks.Add  
xlapp.Visible = False
xlsheet = xlbook.Worksheets(1)                                           'active worksheet
xlsheet.Activate()
xlsheet.Cells(<row>, <col>) = <value>
xlsheet.SaveAs(xlfilename)
xlapp.Quit()
xlapp = Nothing                                                          'release object
```

#### Open Url
```vb
System.Diagnostics.Process.Start(<URL_string>)
```

#### Shell
```vb
Shell(<shell_command>)
```

---

### Design

#### Anchor
Defines the edge of the container to which a certain control is bound. When a control is anchored to an edge, the distance between the control's closetedge and the specified edge will remain constant.

#### Dock
Defines which borders of the control are bound to the container.

#### ComboBox | 选择框
DropDownStyle: Simple, DropDown, DropDownList
```vb
<combobox_name>.SelectedItem
<combobox_name>.Items.Clear()
<combobox_name>.Items.Add(<string>)
```

---

### Project

#### Add Item
Project(right click)->Add->New Item

#### Project Properties
* Startup Object
* Icon

#### Debug / Release

---

## Python

#### Graphviz
[Graphviz - PyPI](https://graphviz.readthedocs.io/en/stable/)
```python
from graphviz import Digraph
...

<graph>=Digraph(...)
<graph>.attr(rankdir=<string>)      #'LR' left-right, 'UD' up-down
<graph>.node(<node_name>)
<graph>.edge(<tail>, <head>, _attributes={'penwidth':'1', 'arrowsize':'1'}})
g.render(view=True, format='png', cleanup=True)
```

#### Argv
```python
import sys
...

sys.argv[]
```

## C++

#### Compile Commands
```C
#pragma once
```
```C
#ifndef _FILENAME_H_
#define

#endif
```

#### Get Path
```C
#include <io.h>
...

long getcwd(char *buf, unsigned long size);
```

#### Convert Between `char*` and `string`
```C
#include <string>
...

string string(char* charPointer);
const char* <string>.c_str();
```
