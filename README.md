# Flow-quest-submission
Flow Cadence September bootcamp 💥

## Chapter 1 - Day 1
- **Q.1 Explain what the Blockchain is in your own words.**

    The Blockchain is an ledger where you store stuff/information such a way that it is nearly impossible to **HACK**.
    Which is not **OWNED** by any authority.
    And a great source to make **MONEY**.
- **Q.2 Explain what a Smart Contract is.**
    
    A Smart Contract is a set of instructions written through CODE by a so called **DEVELOPER**.
    It is fully **TRANSPERENT** means you can see the code of a Smart Contract and see what's happening in it, if you don't understand the contract programming language ***GOD HELP YOU.***
    
- **Q.3 Explain the difference between a script and a transaction.**

  **TRANSACTIONS** : Transaction in simple words means to call a function. When a transaction is called/excuted it **UPDATES** the data/state of the BLOCKCHAIN. For calling/exceution of a transaction the fees is to be paid which is known as **GAS FEES**.
  
  **SCRIPTS** : Script is used to **VIEW** the BLOCKCHAIN. Means It does not change the data or state of the BLOCKCHAIN it just **READS** it. And Scripts do not cost any MONEY for execution.
  
## Chapter 1 - Day 2

- **Q.1 What are the 5 Cadence Programming Language Pillars?**
 
    -  **SAFETY AND SECURITY**

    -  **CLARITY**
    -  **APPROACHABILITY**
    -  **DEVELOPER EXPERIENCE**
    -  **RESOURCE ORIENTED PROGRAMMING**

- **Q.2 In your opinion, even without knowing anything about the Blockchain or coding, why could the 5 Pillars be useful.**


    
    - **SAFETY AND SECURITY** It's very important because there will be users who will deposit there money and it should be SAFE and SECURE
    - **CLARITY** The code should be CLEAR and easy to read. The user should be able to know the intentions of the developer and verify it's SAFETY
    - **APPROACHABILITY** The language should be APROACHABLE so that a user with basic codeing language can also get the idea of what is happening.
    - **DEVELOPER EXPERIENCE** The developer should have good experience with the language/code. It should not **IRRITATE** the dev by not understandable errors.

## Chapter 2 - Day 1
   - **Q.1 Deploy a contract to account `0x03` called "JacobTucker". Inside that contract, declare a constant variable named `is`, and make it have type `String`. Initialize it to "the best" when your contract gets deployed.**

![Screenshot contract (3)](https://user-images.githubusercontent.com/109747152/190894371-57080ad8-c6f0-45d1-bd93-3041034fa716.png)

- **Q.2 Check that your variable `is` actually equals "the best" by executing a script to read that variable. Include a screenshot of the output.**

![Screenshot script](https://user-images.githubusercontent.com/109747152/190894817-7b5b62c0-6f8c-4838-96af-1084b95f95ee.png)

## Chapter 2 - Day 2
 - **Q.1 Explain why we wouldn't call `changeGreeting` in a script.**
  
     Because SCRIPTS only view/reads the data. Therefore we called it in TRANSACTION.
    
 - **Q.2 What does the AuthAccount mean in the prepare phase of the transaction?**
   
     To access the information/data in a account. 
     
- **Q.3 What is the difference between the prepare phase and the execute phase in the transaction?**
       
    **PREPARE PHASE** :  To access the information/data in your account.
    
    **EXECUTE PHASE** : Call function to change the data on the blockchain
    
**CONTRACT EXCERISE**

- **Q.4 A variable named myNumber that has type `Int` (set it to 0 when the contract is deployed)**

**// CONTRACT**
```cadence
pub contract Numbers {
    pub var myNumber: Int

    pub fun updateMyNumber(newNumber: Int) {
      self.myNumber = newNumber
    }

    init() {
        self.myNumber = 0
    }
}
```
- **Q.5 Add a script that reads `myNumber` from the contract**

**// SCRIPT**
```cadence
import Numbers from 0x01

pub fun main(): Int {
    return Numbers.myNumber
}
```
- **Q.6 Add a transaction that takes in a parameter named `myNewNumber` and passes it into the `updateMyNumber` function. Verify that your number changed by running the script again.**

**// TRANSACTION**
```cadence
import Numbers from 0x01

transaction(myNewNumber: Int) {

  prepare(acct: AuthAccount) {}

  execute {
    Numbers.updateMyNumber(newNumber: myNewNumber)
  }
}
```
## Chapter 2 - Day 3

- **Q.1 In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.**

    **I have used "Animes" insted of "people"** 👀
```cadence
    var Animes:[String] = ["Attack on Titan", "Tokyo Revengers", "Naruto"]
    log(Animes)
```
- **Q.2 In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least.**

```cadence
  var Socials: {String: UInt64} = {"Instagram": 7, "Facebook": 0, "Twitter": 10, "Youtube": 8}
  log(Socials)
```

- **Q.3 Explain what the force unwrap operator `!` is.**
    
   - It "UNWRAPS" the optional.Means Unless the thing is **NOT** `nil`, you are **Good to go**
   
- **Q.4 What the error message means, Why we're getting this error, How to fix it.**

    - It means that it is returning an optional.
    - Because we have used dictionaries and dictionaries return optional values.
    - Force unwarp it or change the return type to be an optional.
    
## Chapter 2 - Day 4
 
 - **Q.1 Deploy a new contract that has a Struct of your choosing inside of it.**
 - **Q.2 Create a dictionary or array that contains the Struct you defined.**
 - **Q.3 Create a function to add to that array/dictionary.**
 
 **// CONTRACT**
 ``` cadence
 pub contract Authentication {

    pub var Animes: [Anime]
    
    pub struct Anime {
        pub let name: String
        pub let account: Address

        init(_name: String, _account: Address) {
            self.name = _name
            self.account = _account

        }
    }

    pub fun addCat(name: String, account: Address) {
        let newCat = Anime(_name: name, _account: account)
        self.Animes.append(newCat)
    }

    init() {
        self.Animes = []
    }

}
```
- **Q.4 Add a transaction to call that function.**

**// TRANSACTION**
``` cadence
import Authentication from 0x01

transaction(name: String) {
    let address: Address

    prepare(signer: AuthAccount) {
        self.address = signer.address
    }

    execute {
        Authentication.addCat(name: name, account: self.address)
        log("Anime added.")
    }
}
```
- **Q.5 Add a script to read the Struct you defined.**

**// SCRIPT**
``` cadence
import Authentication from 0x01

pub fun main(index: Int): Authentication.Anime {
    return Authentication.Animes[index]!
}
```
## Chapter 3 - Day 1
 - **Q.1 In words, list 3 reasons why structs are different from resources.**
   
   - They cannot be copied.
   - They cannot be lost.
   - Resources are more secure than structs.

 - **Q.2 Describe a situation where a resource might be better to use than a struct.**
    
    - While making a **Collection of NFTs**.

 - **Q.3 What is the keyword to make a new resource?**
    
    `create` is keyword to make a new resource.
    
 - **Q.4 Can a resource be created in a script or transaction (assuming there isn't a public function to create one)?**
 
    - **NO** It has to be created in the CONTRACT only.
    
 - **Q.5 What is the type of the resource below?**
     
     - `Jacob` is the type of the resource below.
     
 - **Q.6 Let's play the "I Spy" game from when we were kids. I Spy 4 things wrong with this code. Please fix them.**
```cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): Jacob { // there is 1 here
        let myJacob = Jacob() // there are 2 here
        return myJacob // there is 1 here
    }
}
```
**// FIXED**

``` cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob { // there is 1 here
        let myJacob <- create Jacob() // there are 2 here
        return <- myJacob // there is 1 here
    }
}
```
## Chapter 3 - Day 2

- **Q.1 Write your own smart contract that contains two state variables: an array of resources, and a dictionary of resources. Add functions to remove and add to each of them.**

``` cadence
pub contract Anime {

    pub var arrayOfAnimes: @[Animes]
    pub var dictOfAimes: @{String: Animes}

    pub resource Animes {
        pub var topAnimes: String

        init() {
            self.topAnimes = "AOT"
        }
    }

    // Adding anime to an array 
    pub fun addAnime(name: @Animes) {
        self.arrayOfAnimes.append(<- name)
    }

    // Removing anime from an array
    pub fun removeAnime(Index: Int): @Animes {
        return <- self.arrayOfAnimes.remove(at: Index)
    }

    // Adding anime into dictionary
    pub fun addInDict(_name: @Animes) {
        let name = _name.topAnimes
        self.dictOfAimes[name] <-! _name
    }

    // Removing anime from the dictionary
    pub fun removeFromDict(key: String): @Animes {
        let anime <- self.dictOfAimes.remove(key: key)!
        return <- anime
    }

    init() {
        self.arrayOfAnimes <- []
        self.dictOfAimes <- {}
    }
}
```
## Chapter 3 - Day 3

- **Q.1 Define your own contract that stores a dictionary of resources. Add a function to get a reference to one of the resources in the dictionary.**
``` cadence
pub contract Day3 {
    
    pub var dictionary: @{String: something}

    pub resource something {
        pub var favAnime: String

        init(name: String) {
            self.favAnime = name
        }
        
    }

    pub fun refOfSomething(key: String): &something {
        return (&self.dictionary[key] as &something?)!
    }

    init() {
        self.dictionary <- {
            "DEKU": <- create something(name: "My Hero Academia"),
            "EREN": <- create something(name: "Attack On Titan")
        }
    }

}
```

- **Q.2 Create a script that reads information from that resource using the reference from the function you defined in part 1.**

``` cadence
import Day3 from 0x01

pub fun main(): String {
    let ref = Day3.refOfSomething(key: "DEKU")
    return ref.favAnime

}
```
- **Q.3 Explain, in your own words, why references can be useful in Cadence.**
    
    - Reference is a way to  represent something you have. It can be useful in displaying information.
    
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

## Chapter 3 - Day 5

- **Q.1 For today's quest, you will be looking at a contract and a script. You will be looking at 4 variables (a, b, c, d) and 3 functions (publicFunc, contractFunc, privateFunc) defined in SomeContract. In each AREA (1, 2, 3, and 4), I want you to do the following: for each variable (a, b, c, and d), tell me in which areas they can be read (read scope) and which areas they can be modified (write scope). For each function (publicFunc, contractFunc, and privateFunc), simply tell me where they can be called.**

``` cadence
access(all) contract SomeContract {
    pub var testStruct: SomeStruct

    pub struct SomeStruct {

        //
        // 4 Variables
        //

        pub(set) var a: String

        pub var b: String

        access(contract) var c: String

        access(self) var d: String

        //
        // 3 Functions
        //

        pub fun publicFunc() {}

        access(contract) fun contractFunc() {}

        access(self) fun privateFunc() {}


        pub fun structFunc() {
            /**************/
            /*** AREA 1 ***/
            /**************/
        }

        //  A - Read & Write
        //  B - Read & Write
        //  C - Read & Write
        //  D - Read & Write
        
        //  publicFunc, contractFunc and privateFunc



        init() {
            self.a = "a"
            self.b = "b"
            self.c = "c"
            self.d = "d"
        }
    }

    pub resource SomeResource {
        pub var e: Int

        pub fun resourceFunc() {
            /**************/
            /*** AREA 2 ***/
            /**************/
        }

        //  A - Read & Write
        //  B - Read
        //  C - Read
        //  D - No
        
        //  publicFunc, contractFunc

        init() {
            self.e = 17
        }
    }

    pub fun createSomeResource(): @SomeResource {
        return <- create SomeResource()
    }

    pub fun questsAreFun() {
        /**************/
        /*** AREA 3 ****/
        /**************/
    }
        
        //  A - Read & Write
        //  B - Read
        //  C - Read 
        //  D - No
        
         //publicFunc, contractFunc

    init() {
        self.testStruct = SomeStruct()
    }
}

import SomeContract from 0x01

pub fun main() {
  /**************/
  /*** AREA 4 ***/
  /**************/
}

        //  A - Read
        //  B - Read
        //  C - No
        //  D - No
        
         // only publicFunc 
```
 




















 









