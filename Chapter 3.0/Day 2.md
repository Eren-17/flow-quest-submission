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
