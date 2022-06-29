---
layout: default
title: Простая фабрика
parent: Порождающие шаблоны
nav_order: 1
---

# Простая фабрика

Простая фабрика _(англ. simple factory)_

In plain words
> Simple factory simply generates an instance for client without exposing any instantiation logic to the client




Простыми словами
> Простая фабрика просто создает экземпляр для клиента не предоставляя клиенту какой либо логики создания.

[Википедия](https://en.wikipedia.org/wiki/Factory_(object-oriented_programming))
> В объектно-ориентированном программировании (ООП), фабрика - это объект, создающий другие объекты. 
> Формально фабрика это функция или метод, вызов которой возвращает объекты различных классов или прототипов, которые можно считать "новыми".

**Пример кода**

Прежде всего у нас есть интерфейс door и его имплементация
```php
interface Door
{
    public function getWidth(): float;
    public function getHeight(): float;
}

class WoodenDoor implements Door
{
    protected $width;
    protected $height;

    public function __construct(float $width, float $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getWidth(): float
    {
        return $this->width;
    }

    public function getHeight(): float
    {
        return $this->height;
    }
}
```

Затем фабрика DoorFactory создает двери и возвращает их.

```php
class DoorFactory
{
    public static function makeDoor($width, $height): Door
    {
        return new WoodenDoor($width, $height);
    }
}
```

И затем, мы это можем использовать так

```php
$door = DoorFactory::makeDoor(100, 200);
echo 'Width: ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();
```

## Когда использовать?

Если создание объекта не ограничевается парой присвоений и требует вовлечения определенной логики, 
имеет смысл вынести ее в отдельную фабрику вместо постоянного повторения одного и того же кода.


🏠 Simple Factory
--------------

**Programmatic Example**

First of all we have a door interface and the implementation
```php
interface Door
{
    public function getWidth(): float;
    public function getHeight(): float;
}

class WoodenDoor implements Door
{
    protected $width;
    protected $height;

    public function __construct(float $width, float $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getWidth(): float
    {
        return $this->width;
    }

    public function getHeight(): float
    {
        return $this->height;
    }
}
```
Then we have our door factory that makes the door and returns it
```php
class DoorFactory
{
    public static function makeDoor($width, $height): Door
    {
        return new WoodenDoor($width, $height);
    }
}
```
And then it can be used as
```php
// Make me a door of 100x200
$door = DoorFactory::makeDoor(100, 200);

echo 'Width: ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();

// Make me a door of 50x100
$door2 = DoorFactory::makeDoor(50, 100);
```

**When to Use?**

When creating an object is not just a few assignments and involves some logic, it makes sense to put it in a dedicated factory instead of repeating the same code everywhere.
