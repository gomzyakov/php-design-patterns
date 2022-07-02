---
layout: default
title: Простая фабрика
parent: Порождающие шаблоны
nav_order: 1
---

# Простая фабрика _(англ. simple factory)_

Это функция или метод, вызов которой просто создает некоторый объект, не предоставляя какой либо логики создания.

## Когда использовать?

Если создание объекта не ограничевается парой присвоений и требует вовлечения определенной логики,
имеет смысл вынести эту логику в отдельную фабрику вместо постоянного повторения одного и того же кода.

## Простой пример

У нас есть класс `Door`:

```php
class Door
{
    public $width;
    public $height;

    public function __construct(float $width, float $height)
    {
        $this->width = $width;
        $this->height = $height;
    }
}
```

Тогда простая фабрика `DoorFactory` будет создает двери и возвращать их:

```php
class DoorFactory
{
    public static function makeDoor($width, $height): Door
    {
        return new Door($width, $height);
    }
}
```

Создание дверей через фабрику будет выглядеть следующим образом:

```php
$door = DoorFactory::makeDoor(100, 200);
echo 'Width:  ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();
```

## Пример через интерфейс

В простом примере не очень хорошо просматривается зачем вообще нужна простая фабрика, когда
можно зайти через `new Door`.

Немного расширим пример. Доспустим у нас есть интерфейс `Door` и класс деревянной двери `WoodenDoor`:

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

Тогда простая фабрика `DoorFactory` будет создает двери и возвращать их:

```php
class DoorFactory
{
    public static function makeDoor($width, $height): Door
    {
        return new WoodenDoor($width, $height);
    }
}
```

Так будет выглядеть создание дверей:

```php
// Создаст дверь размерами 100x200
$door = DoorFactory::makeDoor(100, 200);

echo 'Width:  ' . $door->getWidth();
echo 'Height: ' . $door->getHeight();

// Создаст дверь размерами 50x100
$small_door = DoorFactory::makeDoor(50, 100);
```

