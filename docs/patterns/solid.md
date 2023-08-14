# SOLID Principles

```{contents}
```

Принципы SOLID - это набор руководящих принципов, разработанных Робертом Мартином, которые способствуют созданию гибкого, расширяемого и поддерживаемого программного кода. Эти принципы призваны улучшить структуру кода, сделать его более устойчивым к изменениям и обеспечить эффективное взаимодействие между различными компонентами системы.

Принципы SOLID составляют аббревиатуру, в которой каждая буква соответствует определенному принципу.

## S - Single Responsibility Principle

> Каждый класс должен иметь только одну причину для изменения. Это означает, что класс должен быть ответственным только за одну функциональность.


```python
class FileManager:
    def read_file(self, file_path):
        # Чтение файла

    def write_file(self, file_path, content):
        # Запись в файл

class EmailSender:
    def send_email(self, to, subject, message):
        # Отправка email

```

В данном случае классы FileManager и EmailSender имеют разные обязанности и могут меняться по разным причинам.

## O - Open/Closed Principle

> Программные сущности (классы, модули, функции и т.д.) должны быть открыты для расширения, но закрыты для модификации. Вместо изменения существующего кода, следует создавать новый код для добавления новой функциональности.


```python
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side ** 2
```

Здесь класс Shape оставлен открытым для расширения путем создания новых классов Circle и Square, но сам Shape не изменяется.

## L - Liskov Substitution Principle

>  Объекты базового класса должны быть заменяемы объектами его производных классов без изменения желаемых свойств программы.

```python
class Bird:
    def fly(self):
        pass

class Sparrow(Bird):
    def fly(self):
        # Реализация полета для воробья

class Ostrich(Bird):
    def fly(self):
        raise Exception("Страус не умеет летать")

def make_bird_fly(bird):
    bird.fly()

sparrow = Sparrow()
ostrich = Ostrich()

make_bird_fly(sparrow)  # Работает
make_bird_fly(ostrich)  # Вызовет исключение, нарушение LSP
```

## I - Interface Segregation Principle

> Клиенты не должны зависеть от интерфейсов, которые они не используют. Лучше создавать несколько узких интерфейсов, чем один общий.


 ```python
 class Worker:
    def work(self):
        pass

class Manager:
    def manage(self):
        pass

class SuperWorker(Worker, Manager):
    def work(self):
        # Реализация работы

    def manage(self):
        # Реализация управления

class RegularWorker(Worker):
    def work(self):
        # Реализация работы

 ```

В данном примере SuperWorker нарушает принцип, так как он зависит от обоих интерфейсов, а RegularWorker следует принципу, завися только от необходимого интерфейса.

## D - Dependency Inversion Principle

Зависимости должны строиться на абстракциях, а не на конкретных реализациях. Модули верхнего уровня не должны зависеть от модулей нижнего уровня, оба должны зависеть от абстракций.

```python
class LightBulb:
    def turn_on(self):
        pass

    def turn_off(self):
        pass

class Switch:
    def __init__(self, bulb):
        self.bulb = bulb

    def operate(self):
        if self.is_on:
            self.bulb.turn_off()
        else:
            self.bulb.turn_on()

```
В данном примере класс Switch зависит от абстракции bulb, что позволяет легко заменять тип лампы без изменения класса Switch.