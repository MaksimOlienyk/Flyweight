# Flyweight - Патерн Проєктування

Патерн Flyweight дозволяє економити пам'ять шляхом розділення спільного стану між об’єктами.  
Об’єкт розділяється на дві частини:
- спільний стан (shared state) — зберігається один раз і кешується,
- унікальний стан (unique state) — передається при виконанні операцій.

## Ідея
Якщо в програмі потрібно створювати багато схожих об’єктів, слід зберігати спільні дані в одній копії об’єкта та повторно її використовувати.

## Структура

| Елемент            | Опис |
|-------------------|------|
| `Flyweight`        | Об’єкт зі спільним станом |
| `FlyweightFactory` | Повертає існуючі flyweight-екземпляри або створює нові при потребі |
| Клієнт            | Передає унікальний стан під час виклику операцій |

## Код

```csharp
class Flyweight {
    string shared;
    public Flyweight(string s) { shared = s; }
    public void Operation(string unique) =>
        Console.WriteLine($"Shared: {shared}, Unique: {unique}");
}

class FlyweightFactory {
    private Dictionary<string, Flyweight> pool = new();
    public Flyweight GetFlyweight(string key) {
        if (!pool.ContainsKey(key))
            pool[key] = new Flyweight(key);
        return pool[key];
    }
}

class Program {
    static void Main() {
        var factory = new FlyweightFactory();
        factory.GetFlyweight("A").Operation("1");
        factory.GetFlyweight("A").Operation("2");
    }
}

