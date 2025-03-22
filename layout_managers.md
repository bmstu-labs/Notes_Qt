**Менеджеры компоновки** (layout managers) представляют возможности для горизонтального, вертикального и табличного размещения виджетов, в том числе и встроенных компоновок. Это означает, что в компоновку вы можете добавить и виджет, и другую компоновку. С помощью этого вы можете собирать компоновки практически любой сложности.

Менеджеры удобны тем, что он сам присваивает виджет-предка помещаемым внутрь себя объектам. Таким образом утечки памяти (memory leak) **не произойдет**. 

**Основные классы** менеджеров компоновки

* `QLayout` - абстрактный класс, унаследованный от `QObject` и `QLayouytItem`
* `QGridLayout` - наследник `QLayout`, управляет табличным размещением
* `QBoxLayout` - наследник `QLayout`, управляет линейным размещением
* `QHBoxLayout` - наследник `QBoxLayout`, размещает виджеты горизонтально
* `QVBoxLayout` - наследник `QBoxLayout`, размещает виджеты вертикально

**Основные методы** 

- `setSpacing()` - устанавливает расстояние между виджетами, принимает количество пикселей
- `setContentMargins()` - устанавливает отступ виджетов от границ сторон компоновки (left, top, bottom, right)
- `addWiddget()` - добавляет виджет в компоновку
- `addLayout()` - добавляет встроенный менеджер компоновки
- `removeWidget()` - удаляет виджет через указатель на него

![Размещение виджетов по горизонтали](images/Widget_Horizontal_Layout.png)

**Пример кода**
```
#include <QtWidgets>

int main(int argc, char **argv) {
   // Application setup
   QApplication app(argc, argv);
	QWidget wgt;
	
	// Buttons setup
	QPushButton *pcmd_a = new QPushButton("Click me");
	QPushButton *pcmd_b = new QPushButton("Not, me!");
	
	// Layout setup
	QBoxLayout *pbxLayout = new QBoxLayout(QBoxLayout::LeftToRight);
	// or more elegant:
	// QHBoxLayout *pbxLayout = new QHBoxLayout();
	pbxLayout->setContentsMargins(10, 10, 10, 10);
	pbxLayout->addWidget(pcmd_a);
	pbxLayout->addWidget(pcmd_b);
	// Set layout to widget
 	wgt.setLayout(pbxLayout);
	
	// Show widget
	wgt.resize(400, 40);
	wgt.show();
	
	// End of program
	return app.exec();
}
```

**Табличное размещение QGridLayout** 
