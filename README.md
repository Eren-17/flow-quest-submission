# Flow-quest-submission
Flow Cadence September bootcamp

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
```
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
```
import Numbers from 0x01

pub fun main(): Int {
    return Numbers.myNumber
}
```
- **Q.6 Add a transaction that takes in a parameter named `myNewNumber` and passes it into the `updateMyNumber` function. Verify that your number changed by running the script again.**

**// TRANSACTION**
```
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
```
    
    var Animes:[String] = ["Attack on Titan", "Tokyo Revengers", "Naruto"]
    log(Animes)
```
- **Q.2 In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least.**
```
  var Socials: {String: UInt64} = {"Instagram": 7, "Facebook": 0, "Twitter": 10, "Youtube": 8}
  log(Socials)
```
- **Q.3 Explain what the force unwrap operator `!` is.**
    
   - It "UNWRAPS" the optional.Means Unless the thing is **NOT** `nil`, you are **Good to go**









