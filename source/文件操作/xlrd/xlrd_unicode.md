# Unicode 处理

该软件包将所有文本字符串显示为 Python unicode 对象。从 Excel 97 开始，Excel 电子表格中的文本已存储为 [UTF-16LE
](http://unicode.org/faq/utf_bom.html/)（16
位Unicode转换格式）。较旧的文件（Excel 95及更早版本）不使用Unicode保留字符串。`CODEPAGE`
 记录提供一个代码页编号（例如1252），xlrd 使用该代码页编号来导出用于转换为 Unicode 的编码（对于同一示例：“cp1252”）。
```python
book = open_workbook('file_path',encoding_override='cp1252')
```

如果 `CODEPAGE` 记录存在但不正确（例如，代码页号为 1251，但字符串实际上是在 koi8_r 中编码的），则可以使用相同的机制来覆盖它。


提供的 runxlrd.py 具有相应的命令行参数，可用于实验：
```shell script
runxlrd.py -e koi8_r 3rows myfile.xls
```
