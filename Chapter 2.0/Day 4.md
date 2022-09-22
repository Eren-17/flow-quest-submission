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
