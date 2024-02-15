# PYTHON: EXCEL
## This note is written for excel operation using Python<br>Written by ***lqy***
## Reference: [CSDN](https://blog.csdn.net/shammy_feng/article/details/124128706)

---
### Module: xlwt
#### Install
```bash
$ pip install xlwt
```

#### Import
```python
import xlwt
```

#### Writing data
1. Establishing a `workbook` object(establish an Excel file):
```python
workbook = xlwt.Workbook(encoding='utf-8',style_compression=0)
#style_compression: whether compressed or not
```

2. Establishing a `sheet` object(establish a sheet):
```python
worksheet = workbook.add_sheet(name,cell_overwrite_ok=True)
#cell_overwrite_ok: whether overwrite the cell, the default value is False
```

3. Add content to `sheet`:
```python
worksheet.write(row,column,value)
#(0,0) refers to row 1, column 1
```

4. Save content
```python
workbook.save(filename)
#remember the .xls postfix
```

#### Data styles
In module `xlwt`, the styles of data are defined by the type `XFStyle`.
1. Fonts
```python{.line-numbers}
import xlwt

workbook = xlwt.Workbook(encoding='utf-8')
worksheet = workbook.add_sheet(name)

style = xlwt.XFStyle()# Initialize styles
font = xlwt.Font()# Establish font for styles

#Some font styles
font.name = '宋'   # Font name
font.height = 300   # Font size is 1:20 in Excel, so 300 here is the NO.15 size font in Excel
font.bold = True    # Whether to bold or not
font.underline = True   # Whether to underline
font.struck_out = True  # Whether to stick out
font.italic = True  # Whether to italic
font.colour_index = 4   # Font colors

# Set font style
style.font = font

# Add data to sheet
worksheet.write(row,column,content) #Add content without sytles
worksheet.write(row,column,content,style) #Add content with styles

workbook.save(filename)
```

Font color index information:
![Font color](https://img-blog.csdnimg.cn/9849cb6781164839b5dc6d72a37467e9.png?x-oss-process%253Dimage%252Fwatermark%252Ctype_d3F5LXplbmhlaQ%252Cshadow_50%252Ctext_Q1NETiBA7pSnIHNoYW1teQ%253D%253D%252Csize_20%252Ccolor_FFFFFF%252Ct_70%252Cg_se%252Cx_16)

2. Pattern styles
Pattern styles means the background color
```python{.line-numbers}
import xlwt

workbook = xlwt.Workbook(encoding='utf-8')
worksheet = workbook.add_sheet(name)

style = xlwt.XFStyle()# Initialize styles

#Establish background pattern
pattern = xlwt.Pattern()
#Set background color
pattern.pattern = xlwt.Pattern.SOLID_PATTERN  # Set background color mode
pattern.pattern_fore_colour = 3    # Set background colour with colour index

style.pattern = pattern # Set background pattern

worksheet.write(row,column,content,style) #Add content with styles

workbook.save(filename)
```

3. Border styles
```python{.line-numbers}
import xlwt

workbook = xlwt.Workbook(encoding='utf-8')
worksheet = workbook.add_sheet(name)

style = xlwt.XFStyle()# Initialize styles

#Establish border
borders = xlwt.Borders()

#Set border values
#Attributes: THIN, DASHED, NO_LINE
borders.left = xlwt.Borders.THIN
borders.right = xlwt.Borders.THIN
borders.top = xlwt.Borders.THIN
borders.bottom = xlwt.Borders.THIN

# Set border pattern
style.borders = borders

worksheet.write(row,column,content,style) #Add content with styles

workbook.save(filename)
```

4. Alignment styles
```python{.line-numbers}
import xlwt

workbook = xlwt.Workbook(encoding='utf-8')
worksheet = workbook.add_sheet(name)

style = xlwt.XFStyle()# Initialize styles

# Set alignment style
alignment = xlwt.Alignment()

# Set alignment attributes
#Vertical alignment and horizontal alignment
alignment.vert = 0x01 # VERT_TOP=0x00; VERT_CENTER=0x01; VERT_BUTTOM=0x02
alignment.horz = 0x03 # HORZ_LEFT=0x01; HORZ_CENTER=0x02; HORZ_RIGHT=0x03

# Change line automatically
alignment.wrap = 1 # Auto-change line

# Set alignment style
style.alignment = alignment

worksheet.write(row,column,content,style) #Add content with styles

workbook.save(filename) #File path is also supported
```

5. num_format_str
The num_format_str means data format attributes
![num_format_str](https://img-blog.csdnimg.cn/16cef4ea93e445c9b90566d765ed9aac.png?x-oss-process%253Dimage%252Fwatermark%252Ctype_d3F5LXplbmhlaQ%252Cshadow_50%252Ctext_Q1NETiBA7pSnIHNoYW1teQ%253D%253D%252Csize_20%252Ccolor_FFFFFF%252Ct_70%252Cg_se%252Cx_16)
```python
import xlwt
from datetime import datetime

workbook  = xlwt.Workbook(encoding='utf-8')
worksheet = workbook .add_sheet(sheetname)

style = xlwt.XFStyle()# Initialize styles

# Example
date_str = '2022-04-12'
num_format_str = 'yyyy/MM/dd'

style.num_format_str = num_format_str # Set style format

# Write the data
worksheet.write(row,column,date_str)
worksheet.write(row,column,datetime.strptime(date_str,'%Y-%m-%d').date(),style)

workbook.save(filename)
```

6. cell size styles
```python
import xlwt

workbook = xlwt.Workbook(encoding='utf-8')
worksheet = workbook.add_sheet(name)

worksheet.col(column).width=width # Set width for column
# Example:
worksheet.col(4).width=256*20 

workbook.save(filename)
```

7. rows and columns combination
Combine several rows and columns together
```python
import xlwt

workbook = xlwt.Workbook(encoding='utf-8')
worksheet = workbook.add_sheet(name)

worksheet.write(column,row,content) # Write data without combinations
worksheet.write_merge(row1,row2,column1,column2,content) # Write data with combinations

# Example:
worksheet.write_merge(0,3,4,7,content) # Row 1 to 4, column E to H are combined together in one cell with content written in it

workbook.save(filename)
```

---
### Module: xlrd
### Module: openpyxl
