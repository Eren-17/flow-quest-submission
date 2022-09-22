## Chapter 3 - Day 4 

- **Q.1 Explain, in your own words, the 2 things resource interfaces can be used for**

    - To specify the requirements to be implemented.
    - It allows to put restrictions.

- **Q.2 Define your own contract. Make your own resource interface and a resource that implements the interface. Create 2 functions. In the 1st function, show an example of not restricting the type of the resource and accessing its content. In the 2nd function, show an example of restricting the type of the resource and NOT being able to access its content**

``` cadence

pub contract BookShop {

  pub resource interface Ibook {
  pub let name: String
  }

  pub resource Book: Ibook {

  pub let name: String

    pub fun getBook(): String {
      return "Read Manga"
    }

    init(_name: String) {
      self.name = _name
    }
  }

  // Allows Access
  pub fun createBook(name: String): @Book {
    return <- create Book(_name: name)
  }

  // Access Restricted
  pub fun createIBook(name: String): @Book{Ibook} {
    return <- create Book(_name: name)
  }

   
}
```

- **Q.3 How would we fix this code?**
``` cadence
pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String

      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") // ERROR HERE: `member of restricted type is not accessible: changeGreeting`
      log(newGreeting)
    }
}
```
**// FIXED**
``` cadence

pub contract Stuff {

    pub struct interface ITest {
      pub var greeting: String
      pub var favouriteFruit: String

      //Added the changeGreeting function
      pub fun changeGreeting(newGreeting: String): String
    }

    // ERROR:
    // `structure Stuff.Test does not conform 
    // to structure interface Stuff.ITest`
    pub struct Test: ITest {
      pub var greeting: String
      pub var favouriteFruit: String   // Added the favouriteFruit variable
      pub fun changeGreeting(newGreeting: String): String {
        self.greeting = newGreeting
        return self.greeting // returns the new greeting
      }

      init() {
        self.greeting = "Hello!"
        self.favouriteFruit = "Devil Fruit!" 
      }
    }

    pub fun fixThis() {
      let test: Test{ITest} = Test()
      let newGreeting = test.changeGreeting(newGreeting: "Bonjour!") 
      log(newGreeting)
    }
}
```
