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
