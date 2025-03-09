# Interface vs Abstract Class in C#

Both help create a "template" for other classes, but they work differently:

## Interface
* Like a contract that says "any class using me MUST include these methods"
* Contains only method names - no actual code inside methods
* Classes can use MULTIPLE interfaces
* All methods in interface must be implemented

```csharp
// Multiple interfaces
interface IAnimal
{
    void MakeSound();
    void Move();
}

interface IPet
{
    string Name { get; set; }
    void Play();
}

interface ITrainable
{
    void LearnTrick(string trick);
    List<string> GetTricks();
}

// One class implementing MULTIPLE interfaces
class Dog : IAnimal, IPet, ITrainable
{
    public string Name { get; set; }
    private List<string> tricks = new List<string>();
    
    public void MakeSound()
    {
        Console.WriteLine("Woof!");
    }
    
    public void Move()
    {
        Console.WriteLine("Running");
    }
    
    public void Play()
    {
        Console.WriteLine($"{Name} plays fetch!");
    }
    
    public void LearnTrick(string trick)
    {
        tricks.Add(trick);
    }
    
    public List<string> GetTricks()
    {
        return tricks;
    }
}
```

## Abstract Class
* Like a partially built class - has some finished parts, some empty parts
* Can contain both method names AND completed methods with code
* Classes can only use ONE abstract class
* Some methods can be left for child classes to fill in

```csharp
abstract class Animal
{
    public void Breathe()  // Complete method - ready to use
    {
        Console.WriteLine("Breathing...");
    }
    
    public abstract void MakeSound();  // Empty method - must be filled in
}

class Cat : Animal
{
    public override void MakeSound()  // Must provide code for abstract methods
    {
        Console.WriteLine("Meow!");
    }
    // Cat gets Breathe() method automatically
}
```

## When to use which?
* Use **interface** when classes need to follow a specific pattern but might be very different from each other
* Use **abstract class** when classes share some common behaviors but need to customize others
