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
