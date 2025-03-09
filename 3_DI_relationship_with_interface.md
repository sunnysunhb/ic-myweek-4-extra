# Dependency Injection & How It Relates to Interfaces

Dependency injection is a way to provide objects that a class needs (dependencies) from the outside instead of having the class create them itself.

## What is Dependency Injection?

Think of it like this:
- **Without DI**: A chef buys their own ingredients at the store
- **With DI**: Someone else brings ingredients to the chef

```csharp
// WITHOUT dependency injection
class ZooKeeper
{
    private Dog animal; // ZooKeeper creates its own specific animal
    
    public ZooKeeper()
    {
        animal = new Dog(); // Hard-coded to use Dog
    }
    
    public void FeedAnimal()
    {
        animal.MakeSound();
    }
}
```

```csharp
// WITH dependency injection
class ZooKeeper
{
    private IAnimal animal; // Uses interface instead of specific class
    
    public ZooKeeper(IAnimal anyAnimal) // Animal is "injected" from outside
    {
        animal = anyAnimal;
    }
    
    public void FeedAnimal()
    {
        animal.MakeSound();
    }
}

// Now you can use it with any IAnimal
var keeper1 = new ZooKeeper(new Dog());
var keeper2 = new ZooKeeper(new Cat());
```

## How This Relates to Interfaces

Interfaces make dependency injection work better because:

1. **Flexibility**: ZooKeeper can work with any class that implements IAnimal
2. **Testing**: Easy to inject test versions of dependencies
   ```csharp
   var testAnimal = new TestAnimal();
   var keeper = new ZooKeeper(testAnimal);
   keeper.FeedAnimal();
   // Now check if testAnimal was used correctly
   ```
3. **Loose Coupling**: ZooKeeper doesn't need to know the exact type of animal
4. **Swappable Components**: Can swap implementations without changing ZooKeeper

Dependency injection and interfaces work together to make your code more flexible and easier to test.
