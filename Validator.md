# Проверка ввода
Объект класса `QValidator` (контролер или валидатор) гарантирует правильность ввода пользователя, согласно указанным в классе требованиям

Для установки контролера достаточно передать его в метод `setValidator()`, который содержится в классах `QComboBox` и `QLineEdit`

Для проверки ввода чисел существуют готовые классые `QIntValidator` и `QDoubleValidator`

Создавая собственный класс проверки, его нужно унаследовать от `QValidator` и перезаписать метод `validate(QString&, int&)`, в который передается вводимая строка и позиция курсора. Метод возвращает следующие значения:
- `QValidator::Invalid` - если строка не может быть принята
- `QValidator::Intermediate` - если строка не может быть принята в качестве результата (например, установлен диапазон от 50 до 100; в таком случае, ввод единицы представляет промежуточное значение)
- `QValidator::Acceptable` - значение можно принять без изменений

### Пример кода

```
#include <QtWidgets>

class NameValidator : public QValidator {
public:
	NameValidator(QObject *parent) : QValidator(parent) {}
	
	virtual QValidator::State validate(QString &str, int &pos) const {
		QRegExp rxp = QRegExp("[0-9]");
		if (str.contains(rxp)) {
			return QValidator::Invalid;
		}
		return QValidator::Acceptable;
	}
};

int main(int argc, char **argv) {
	QApplication app(argc, argv);
	QWidget wgt;
	
	// Widgets set up
	auto plbl = new QLabel("Name");
	auto ptxt = new QLineEdit;
	
	// Validator set up
	auto pnmv = new NameValidator(ptxt);
	ptxt->setValidator(pnmv);
	plbl->setBuddy(ptxt);
	
	// Layout set up
	auto pb = new QVBoxLayout;
	pb->addWidget(plbl);
	pb->addWidget(ptxt);

	wgt.setLayout(pb);
	wgt.show();

	return app.exec();
}
```