## Механизм закулисного хранения (Backing store)
Техника заключается в растровых изображений для всех виджетов окна в памяти компьютера. Позволяет повысить производительность через ограничение использование вычислений при рисовании

## Установка фона виджета
Сначала требуется создать объект палитры, а затем вызвать метод `setPalette()` для установки его в виджете.

Чтобы все потомки заполнялись фоном и были видимы, нужно установить свойство `autoFillBackground` равным `true`.
```
wgt.setAutoFillBackground(true);
```

Пример кода
```
int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    QWidget wgt;

    // Заливка цветом
    QWidget *pwgt_color = new QWidget(&wgt);
    QPalette palette_color;
    palette_color.setColor(pwgt_color->backgroundRole(), Qt::blue);
    pwgt_color->setPalette(palette_color);
    pwgt_color->resize(100, 100);
    pwgt_color->move(25, 25);
    pwgt_color->setAutoFillBackground(true);

    // Заливка изображением
    QWidget *pwgt_image = new QWidget(&wgt);
    QPalette palette_image;
    palette_image.setBrush(pwgt_image->backgroundRole(), QBrush(QPixmap("./image.jpg")));
    pwgt_image->setPalette(palette_image);
    pwgt_image->resize(100, 100);
    pwgt_image->move(75, 75);
    pwgt_image->setAutoFillBackground(true);

    // Отображение виджета
    wgt.resize(200, 200);
    wgt.show();

    return app.exec();
}
```

## Изменение курсора
Курсор имеет собственный класс - `QCursor`. Установить свое изображение курсора можно методом `setCursor()`, передав ему объект класса `QPixmap` или значения из пространства имет Qt, вот некоторые из них:
- `Qt::ArrowCursor` (стандартная стрелка)
- `Qt::PointingHandCursor` (указатель в виде руки)
- `Qt::WaitCursor` (песочные часы, для ожидания)

Вызов статического метода `QGuiApplication::setOverrideCursor()` устанавливает картинку курсора для всего приложения. Метод `QGuiApplication::restoreOverrideCursor()` возвращает предыдущее изображение курсора.

Пример кода изменения курсора
```
int main(int argc, char **argv) {
	QApplication app(argc, argv);
	QWidget wgt;
	
	// Проверить наличие файла можно через QFile::exists("file_path"). Возвращает true/false 
	QPixmap pix("/image.jpg");
	QCursor cursor(pix);

	wgt.setCursor(cursor);
	wgt.resize(200, 200);
	wgt.show();
	
	return app.exec();
}
```
