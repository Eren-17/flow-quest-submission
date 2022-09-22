## Chapter 4 - Day 1

- **Q.1 Explain what lives inside of an account.**
    
    - **Contract code** and **Account Storage**.

- **Q.2 What is the difference between the /storage/, /public/, and /private/ paths?**.

    - `/storage` is the place where all of the things you own actually lives.
    
    - `/public` and `/private` links to storage and helps to access it the way you want.
    
- **Q.3 What does `.save()` do? What does `.load()` do? What does `.borrow()` do?**

    - `.save()` :- saves a resource into account storage.
    
    - `.load()` :- takes out a resource from the account storage.
    
    - `.borrow()` :- borrow's reference of a resource from the account storage.
    
- **Q.4 Explain why we couldn't save something to our account storage inside of a script.**

    - Access to AuthAccount is require to save something in account storage and in script we can't get access to AuthAccount.
    
- **Q.5 Explain why I couldn't save something to your account.**

    - Because you would need the AuthAccount access or else you can't save.
    
- **Q.6 Define a contract that returns a resource that has at least 1 field in it. Then, write 2 transactions:**
``` cadence
pub contract storage {

    pub resource Hello {
        pub var name: String

        init() {
            self.name = "EREN"
        }
    }

    pub fun createHello(): @Hello {
        return <- create Hello()
    }

}
```

- **A transaction that first saves the resource to account storage, then loads it out of account storage, logs a field inside the resource, and destroys it.**
``` cadence
import storage from 0x01

transaction {

  prepare(signer: AuthAccount) {
    let new <- storage.createHello()

    signer.save(<- new, to: /storage/HelloResource)

    let newLoad <- signer.load<@storage.Hello>(from: /storage/HelloResource)
                    ?? panic("The thing you are looking for is not here!")
                    log (newLoad.name)

                    destroy  newLoad

  }

  execute {
    
  }
}
```
- **A transaction that first saves the resource to account storage, then borrows a reference to it, and logs a field inside the resource.**
``` cadence
import storage from 0x01

transaction {

  prepare(signer: AuthAccount) {
    let new <- storage.createHello()

    signer.save(<- new, to: /storage/HelloResource)

    let newborrow = signer.borrow<&storage.Hello>(from: /storage/HelloResource)
                    ?? panic("it's not here")
                    log(newborrow.name)

  }

  execute {
    
  }
}
```
