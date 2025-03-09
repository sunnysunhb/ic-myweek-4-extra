# Why Use Interfaces?

Interfaces are useful for several important reasons:

## 1. Testing
```csharp
interface IAnimal
{
    void MakeSound();
    void Move();
}
```

For testing, interfaces are perfect because:
- You can create "fake" test versions of classes
- Example: When testing a `ZooKeeper` class that works with `IAnimal`, you can create a simple `TestAnimal` that implements `IAnimal` without needing real animals

```csharp
class TestAnimal : IAnimal
{
    public string SoundMade { get; private set; }
    
    public void MakeSound()
    {
        SoundMade = "Test sound";
    }
    
    public void Move() 
    {
        // Simple test implementation
    }
}

// Now you can test if ZooKeeper correctly calls MakeSound()
```

## 2. Flexibility
- Different classes can work together even if they're not related
- Example: Both `Dog` and `Robot` can implement `IAnimal` even though they're very different

## 3. Code Organization
- Helps define clear "roles" that classes can play
- Makes your code easier to understand

## 4. Plug-and-Play Components
- You can swap implementations without changing other code
- Example: Change from `RealDatabase` to `CloudDatabase` if both implement `IDatabase`

In the real world, interfaces help you create systems where parts can be easily replaced or updated without breaking everything else.
