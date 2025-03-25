# Электронный индикатор
Класс `QLCDNumber` определен в заголовочном файле QLCDNumber. По внешнему виду представляет собой набор сегментных указателей - прямо как на электронных часах или калькуляторах.

С помощью `QLCDNumber` удобно отображать целые числа. Допускается использование точки с помощью специального метода.

### Основные методы
- `display(double)` - помещает `num` на дисплей\
- `setSegmentStyle(QLCDNumber::SegmentStyle)` - устаналивает стиль сегментов (`QLCDNumber::Flat` самый популярный)
- `value()` - возвращает значение с дисплея типа `double`
- `setSmallDecimalPoint(bool)` - если `true`, устанавливает небольшую дробную точку. В противном случае точка занимает 1 сегмент
- `setMode(QLCDNumber::Mode)` - устанавливает режим отображения числа: `QLCDNumber::Hex`, `QLCDNumber::Dec`, `QLCDNumber::Oct`, `QLCDNumber::Bin`

### Сигналы
- `overflow()` - вызывается при выходе числа за количество сегментов

### Пример кода
**Примечание:** на версии 5.15.15 Qt Creator может выдавать очень странные ошибки при импорте `QLCDNumber`. Если вы встретились с такой проблемой, то используйте импорт всех виджетов: `QtWidgets`. 

```
#include <QWidget>
#include <QApplication>
#include <QLCDNumber>
#include <QSpinBox> 

int main(int argc, char **argv) {
    QApplication app(argc, argv);
    QWidget wgt;
	
    // Create and set up LCD Display
    QLCDNumber *plcd = new QLCDNumber(4);
	 plcd->setSegmentStyle(QLCDNumber::Filled);
    plcd->setMode(QLCDNumber::Hex);
	 
	 // Create and set up SpinBox
    QSpinBox *pspb = new QSpinBox;
    pspb->setFixedHeight(30);
    pspb->setMaximum(999);
	 
	 // Connect slot display to signal valueChanged
	 // to display the value from SpinBox instantly as it changes
    QObject::connect(pspb, SIGNAL(valueChanged(int)), plcd, SLOT(display(int)));

	 // Create and set up layout manager
    QVBoxLayout *pvbxLayout = new QVBoxLayout;
    pvbxLayout->addWidget(plcd);
    pvbxLayout->addWidget(pspb);

    wgt.setLayout(pvbxLayout);
    wgt.resize(250, 150);

    wgt.show();
    app.exec();
}
```