## Chapter 4 - Day 2

- **Q.1 What does `.link()` do?**
    
    - It points to resource stored in `/storage`. And helps you to make it more restrictive by using `/public` or `/private`
    
- **Q.2 In your own words (no code), explain how we can use resource interfaces to only expose certain things to the /public/ path.**

    - Resource Interfaces comes handy while createing more restrictive types of resource's. And can also use it to restrict the capability.
    
- **Q.3 Deploy a contract that contains a resource that implements a resource interface.**
``` cadence
pub contract Day2 {

    pub resource interface IHello {
        pub var name: String
        pub var age: UInt64
    }

    pub resource Hello: IHello {
        pub var name: String
        pub var age: UInt64
        pub var anime: String

        init() {
            self.name = "EREN"
            self.age = 17
            self.anime = "Attack On Titan"

        }
    }

    pub fun createHello(): @Hello {
        return <- create Hello()
    }

}
```

- **In a transaction, save the resource to storage and link it to the public with the restrictive interface.**
``` cadence
import Day2 from 0x01

transaction {

  prepare(signer: AuthAccount) {
    let new <- Day2.createHello()

    signer.save(<- new, to: /storage/Hello)

    signer.link<&Day2.Hello{Day2.IHello}>(/public/Day2, target: /storage/Hello)
    log("Resource stored and linked")

  }

  execute {
    
  }
}
```
- **Run a script that tries to access a non-exposed field in the resource interface, and see the error pop up.**
``` cadence
import Day2 from 0x01

pub fun main(address: Address): String  {
  let publicCapability: Capability<&Day2.Hello{Day2.IHello}> = 
      getAccount(address).getCapability<&Day2.Hello{Day2.IHello}>(/public/Day2)
  
  let hello: &Day2.Hello{Day2.IHello} = publicCapability.borrow()
            ?? panic("The capability does'nt exist, or the path is wrong")

    // Error: member of restricted type is not accessible: anime

  return hello.anime 
}
```
- **Run the script and access something you CAN read from. Return it from the script.**
``` cadence
import Day2 from 0x01

pub fun main(address: Address): String  {
  let publicCapability: Capability<&Day2.Hello{Day2.IHello}> = 
      getAccount(address).getCapability<&Day2.Hello{Day2.IHello}>(/public/Day2)
  
  let hello: &Day2.Hello{Day2.IHello} = publicCapability.borrow()
            ?? panic("The capability does'nt exist, or the path is wrong")

    // Result > {"type":"String","value":"EREN"}

  return hello.name
}
```
