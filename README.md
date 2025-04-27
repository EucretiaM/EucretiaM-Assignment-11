Assignment 11: Implementing a Persistence
Repository Layer

Objective:
Design and implement a repository layer to persist your domain model objects.

The generic repository pattern is a lifesaver for keeping data access code clean and reusable. Its consistency not only simplifies maintenance but also boosts productivity in scalable applications.

The differences between Dependency Injection and Factory Pattern

What is the Dependency Injection (DI) Pattern?
The Dependency Injection (DI) pattern is a design pattern used in software engineering to manage dependencies between objects. In DI, instead of a class creating its dependencies internally, these dependencies are provided to the class from an external source. This allows for greater flexibility, easier testing, and improved maintainability of the codebase.

Flexibility: Classes become more flexible as they can easily switch between different implementations of dependencies.
Testability: Dependency Injection facilitates easier unit testing, as dependencies can be easily replaced with mock objects.
Maintainability: Code becomes easier to maintain and extend, as changes to dependencies can be made externally without modifying the class itself

Example

class Car
{
    private Engine engine;
    private SteeringWheel wheel;
    private Tires tires;

    public Car(Engine engine, SteeringWheel wheel, Tires tires)
    {
        this.engine = engine;
        this.wheel = wheel;
        this.tires = tires;
    }
}



What is the Factory Pattern?
The Factory Method Design Pattern is a creational design pattern used in software engineering to provide an interface for creating objects in a superclass, while allowing subclasses to alter the type of objects that will be created.

It encapsulates the object creation logic in a separate method, abstracting the instantiation process and promoting loose coupling between the creator and the created objects.
This pattern enables flexibility, extensibility, and maintainability in the codebase by allowing subclasses to define their implementation of the factory method to create specific types of objects.

Example

static class CarFactory
{
    public ICar BuildCar()
    {
        Engine engine = new Engine();
        SteeringWheel steeringWheel = new SteeringWheel();
        Tires tires = new Tires();
        ICar car = new RaceCar(engine, steeringWheel, tires);
        return car;
    }   
}
