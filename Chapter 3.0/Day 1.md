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
