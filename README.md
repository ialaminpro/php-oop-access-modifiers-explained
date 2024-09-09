## **PHP OOP - Access Modifiers**

In PHP Object-Oriented Programming (OOP), **access modifiers** control the visibility of class properties and methods. The primary access modifiers in PHP are `public`, `protected`, and `private`. Understanding these modifiers is crucial for encapsulating and managing the behavior of classes effectively.

### **1. Public Access Modifier**

- **Keyword**: `public`
- **Visibility**: Accessible from anywhere—inside the class, outside the class, and in derived classes.
- **Use Case**: Use `public` for properties or methods that should be accessible from any context.

#### Example:
```php
class User {
    public $name = "John";
    
    public function greet() {
        return "Hello, " . $this->name;
    }
}

$user = new User();
echo $user->greet();  // Output: Hello, John
```

In this example, both the property `$name` and the method `greet()` are public, allowing them to be accessed directly from outside the class.

### **2. Protected Access Modifier**

- **Keyword**: `protected`
- **Visibility**: Accessible within the class itself and by subclasses (child classes), but **not from outside** the class.
- **Use Case**: Use `protected` to allow derived classes to access certain properties or methods while keeping them hidden from external code.

#### Example with Correct Access:
```php
class Person {
    protected $age = 30;

    protected function getAge() {
        return $this->age;
    }
}

class Employee extends Person {
    public function showAge() {
        return $this->getAge();  // Correct: Accesses protected method within a subclass
    }
}

$employee = new Employee();
echo $employee->showAge();  // Output: 30
```

In this example, `getAge()` is a protected method, which is accessible within the `Employee` class, a subclass of `Person`.

#### Example with Error:
```php
class Person {
    protected $age = 30;

    protected function getAge() {
        return $this->age;
    }
}

$person = new Person();
echo $person->getAge();  // Error: Cannot access protected method Person::getAge()
```

**Error Message**: `Fatal error: Uncaught Error: Cannot access protected method Person::getAge()`

In this case, trying to access the protected method `getAge()` directly from an instance of `Person` results in an error because protected methods are not accessible from outside the class.

### **3. Private Access Modifier**

- **Keyword**: `private`
- **Visibility**: Only accessible within the class where it is defined. **Not accessible** from subclasses or external code.
- **Use Case**: Use `private` to hide properties or methods from any code outside the class, including derived classes.

#### Example with Correct Access:
```php
class BankAccount {
    private $balance = 1000;

    private function getBalance() {
        return $this->balance;
    }

    public function showBalance() {
        return $this->getBalance();  // Correct: Accesses private method within the same class
    }
}

$account = new BankAccount();
echo $account->showBalance();  // Output: 1000
```

In this example, the `getBalance()` method is private, so it can only be accessed within the `BankAccount` class. The `showBalance()` method is public and can be used to indirectly access the private `getBalance()`.

#### Example with Error:
```php
class BankAccount {
    private $balance = 1000;

    private function getBalance() {
        return $this->balance;
    }
}

$account = new BankAccount();
echo $account->getBalance();  // Error: Cannot access private method BankAccount::getBalance()
```

**Error Message**: `Fatal error: Uncaught Error: Cannot access private method BankAccount::getBalance()`

In this case, trying to access the private method `getBalance()` directly from an instance of `BankAccount` results in an error because private methods are not accessible from outside the class.

#### Example with Error in Subclass:
```php
class BankAccount {
    private $balance = 1000;

    private function getBalance() {
        return $this->balance;
    }
}

class SavingsAccount extends BankAccount {
    public function showBalance() {
        return $this->getBalance();  // Error: Cannot access private method BankAccount::getBalance()
    }
}

$savings = new SavingsAccount();
echo $savings->showBalance();
```

**Error Message**: `Fatal error: Uncaught Error: Cannot access private method BankAccount::getBalance()`

Here, the private method `getBalance()` is inaccessible even to subclasses like `SavingsAccount`, demonstrating that private methods cannot be accessed outside their defining class.

### **4. Summary of Access Modifiers**

| Modifier    | Inside Class | Derived Class | Outside Class |
|-------------|--------------|---------------|---------------|
| **Public**  | Yes          | Yes           | Yes           |
| **Protected** | Yes        | Yes           | No            |
| **Private** | Yes          | No            | No            |

### **5. Best Practices**

- Use **`public`** sparingly to expose only what is necessary. Prefer encapsulation and expose functionality via public methods.
- Use **`protected`** to allow subclasses to access necessary properties or methods while hiding them from external code.
- Use **`private`** to fully encapsulate class internals and prevent access from outside or derived classes.

### **Conclusion**

PHP's access modifiers (`public`, `protected`, `private`) provide a mechanism to manage visibility and encapsulation in OOP. By understanding and applying these modifiers correctly, you can create more secure and maintainable code.
