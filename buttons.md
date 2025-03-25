# Кнопки
`QPushButton` - основной класс для кнопок.  его конструктор передается строка, которая задает надпись кнопки.

К кнопке также можно подключить меню - объект класса `QMenu`. Для этого следует создать такой объект на основе кнопки и соединить его с кнопкой через метод `QPushButton::setMenu(&QMenu)`.

### Варианты кнопок
- **Normal Button** - самая обычная кнопка. После отпускания возвращается в исходное положение
- **Toggle Button** (Выключатель) - может иметь 2 состояние: нажата, отжата
- **Flat Button** (Плоская кнопка) - по функциональности идентична обычной кнопки. Единственное отличие - отсутствие контуров. Полезна для размещения "скрытой кнопки"
- **Pixmap Button** - кнопка, содержащая растровое изображение (вместе с текстом)

### Основные сигналы
- `clicked()` - отпраляется при щелчке кнопки
- `pressed()` - отправляется при нажатии кнопки
- `released()` - отправляется при отпускании кнопки
- `toggled()` - отправляется при изменении состояния кнопки-выключателя

### Опрос состояния
- `isDown()` - возвращает `true`, если кнопка в нажатом состоянии
- `isChecked()` - возвращает `true`, если кнопка во включенном состоянии
- `isEnabled()` - возвращает `true`, если кнопка доступна

### Пример кода
```
#include <QApplication>
#include <QWidget>
#include <QPushButton>
#include <QVBoxLayout>
#include <QMenu>

int main(int argc, char **argv) {
	QApplication app(argc, argv);
	QWidget *wgt = new QWidget;
	
	// Set up normal button
	QPushButton *pcmdNormal = new QPushButton("Normal Button");
	
	// Set up toggle button
	QPushButton *pcmdToggle = new QPushButton("Toggle Button");
	pcmdToggle->setCheckable(true);
	pcmdToggle->setChecked(true);

	// Set up flat button
	QPushButton *pcmdFlat = new QPushButton("Flat Button");
	pcmdFlat->setFlat(true);

	// Set up pixmap button. An image required
	QPixmap pix(":/img.png");
	QPushButton *pcmdPix = new QPushButton("Pixmap Button");
	pcmdPix->setIcon(pix);
	pcmdPix->setIconSize(pix.size());

	// Set up menu button
	QPushButton *pcmdMenuButton = new QPushButton("Menu Button");
	QMenu *pmnu = new QMenu(&pcmdMenuButton);
	pmnu->addAction("Item1");
	pmnu->addAction("Item2");
	pmnu->addAction("Quit", &app, SLOT(quit()));

	pcmdMenuButton->setMenu(pmnu);

	// Layout setup
	QVBoxLayout *pvbx = new QVBoxLayout;
	pvbx->addWidget(pcmdNormal);
	pvbx->addWidget(pcmdToggle);
	pvbx->addWidget(pcmdFlat);
	pvbx->addWidget(pcmdPix);
	pvbx->addWidget(pcmdMenuButton);
	
	wgt->setLayout(pvbx);
	wgt->show();
	
	return app.exec();
}
```