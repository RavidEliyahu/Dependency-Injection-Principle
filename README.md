# Dependency-Injection-Principle

## An example before using di:

In the RPG adventure game, there is a character class that represents the player character. The character class has a method called "Attack()" which calculates and applies damage to a target enemy. The character class also has a property called "Weapon" which is an instance of a weapon class that represents the weapon the character is using. The weapon class has a method called "CalculateDamage()" which calculates the damage that the weapon does.
```cs
public class Character
{
    public Weapon Weapon { get; set; }

    public void Attack(Enemy enemy)
    {
        int damage = Weapon.CalculateDamage();
        enemy.Health -= damage;
    }
}
```
The problem with this implementation is that the character class is tightly coupled to the weapon class. This means that the character class depends on the specific implementation of the weapon class and cannot be easily tested or reused with other weapon classes.

## Fixed version using dependency injection:

To fix this issue, we can use dependency injection to decouple the character class from the weapon class. This involves injecting the weapon class as a dependency into the character class through its constructor, like this:
```cs
public class Character
{
    private readonly IWeapon _weapon;

    public Character(IWeapon weapon)
    {
        _weapon = weapon;
    }

    public void Attack(Enemy enemy)
    {
        int damage = _weapon.CalculateDamage();
        enemy.Health -= damage;
    }
}
```
Now, the character class depends on an interface called "IWeapon" rather than a specific implementation of the weapon class. This allows us to easily test the character class with different weapon classes, and it also makes it easier to reuse the character class in different contexts.
To use this implementation, we can create an instance of the character class like this:
```cs
IWeapon weapon = new Sword();
Character character = new Character(weapon);
character.Attack(enemy);
```
In this example, we have injected an instance of the Sword class (which implements the IWeapon interface) into the character class. This allows the character class to use any class that implements the IWeapon interface, without being tightly coupled to a specific implementation.
