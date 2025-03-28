# Однострочное текстовое поле
Класс `QLineEdit` определен в одноименном заголовочном файле.

Этот виджет следует использовать в случаях, когда требуется вводить не более одной строки текста

### Основные методы
- `text()` - получение текста в виджете в формате `QString`
- `setReadOnly(bool)` - отключение возможности менять текст
- `setText(QString)` - помещение текста в виджет
- `setEchoMode(bool` - сокрытие вводимых символов символов *
- `setMaxLength(int)` - установка максимального количество символов в строке (поштучно)

### Сигналы
- `textChanged(const QString&)` - реагирует на любое изменение текста в виджете
- `textEdited(const QString&)` - реагирует только на изменение текста пользователем
- `cursorPositionChanged(int, int)` - реагирует на смещение курсора. Передает старую и новую позицию соответственно

### Слоты
- `clear()` - очищение строки
- `copy()` - копирование текста в буфер обмена
- `cut()` - копирование текста в буфер обмена и очищение строки
- `paste()` - вставка текста из буфера обмена
- `redo()` - повторение последней отмененной операции
- `selectAll()` - выделение всего текста и перемещение курсора в конец
- `setText(const QString&)` - установить переданный текст
- `undo()` - отменить последюю операцию

### Пример программы
```
#include <QtWidgets>

int main(int argc, char **argv) {
	QApplication app(argc, argv);
	QWidget wgt;
	
	// Create main display. It will display text is being edited
	QLabel *plblDisplay = new QLabel;
	plblDisplay->setFrameStyle(QFrame::Box | QFrame::Raised);
	plblDisplay->setLineWidth(2);
	plblDisplay->setFixedHeight(50);
	
	// Create edit line with label
	QLabel *plblText = new QLabel("Text");
	QLineEdit *ptxt = new QLineEdit;
	plblText->setBuddy(ptxt);
	QObject::connect(ptxt, SIGNAL(textChanged(const QString&)), plblDisplay, SLOT(setText(const QString&)));
	
	// Create edit line with password style (widget will hide chars)
	QLabel *plblPassword = new QLabel("Password");
	QLineEdit *ptxtPassword = new QLineEdit;
	plblPassword->setBuddy(ptxtPassword);
	ptxtPassword->setEchoMode(QLineEdit::Password);
	QObject::connect(ptxtPassword, SIGNAL(textChanged(const QString&)), plblDisplay, SLOT(setText(const QString&)));
	
	// Create auto layout
	// The keyword auto might be used here instead of QVBoxLayout*
	QVBoxLayout *pb = new QVBoxLayout;
	pb->addWidget(plblDisplay);
	pb->addWidget(plblText);
	pb->addWidget(ptxt);
	pb->addWidget(plblPassword);
	pb->addWidget(ptxtPassword);

	wgt.setLayout(pb);
	wgt.show();
	
	return app.exec();
}
```
