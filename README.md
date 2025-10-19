# Flyweight
```cs
class Flyweight {
    string shared;
    public Flyweight(string s){shared=s;}
    public void Operation(string unique)=>Console.WriteLine($"Shared: {shared}, Unique: {unique}");
}

class FlyweightFactory {
    private Dictionary<string, Flyweight> pool=new();
    public Flyweight GetFlyweight(string key){
        if(!pool.ContainsKey(key)) pool[key]=new Flyweight(key);
        return pool[key];
    }
}

class Program {
    static void Main(){
        var factory=new FlyweightFactory();
        factory.GetFlyweight("A").Operation("1");
        factory.GetFlyweight("A").Operation("2");
    }
}
