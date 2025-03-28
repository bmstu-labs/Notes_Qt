# Запись в файл
Класс `QTextDocumentWriter` предоставляет три формата для записи содержимого класса `QTextDocument`: в PlainText, в HTML и ODF (Open Document Format)

Для записи файла в конкретном формате необходимо передать строку с форматов в метод `setFormat()`

```cpp
QTextEdit *ptxt = new QTextEdit("This is a <b>TEST<\b>");
QTextDocumentWriter writer;

writer.setFormat("odf");
writer.setFileName("output.odf");
writer.write(ptxt->document());
```

### Запись в формате PDF
Запись в формат PDF классом `QTextDocumentWriter` не поддерживается, но ее можно осуществить путем рисования в контексте `QPrinter`

```cpp
QTextEdit *ptxt = new QTextEdit("This is a <b>TEST<\b>");
QPrinter printer(QPrinter::HighResolution);
printer.setOutputFormat(QPrinter::PdfFormat);
printer.setOutputFileName("out.pdf");
ptxt->document()->print(&printer);
```

Также для создания PDF-файлов можно использовать класс `QPdfWriter`

**Примечание:** класс QPrinter находится в модуле `QtPrinterSupport`, поэтому для его использования необходимо добавить в проектный файл строку `QT += printsupport`