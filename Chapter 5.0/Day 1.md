## Chapter 5 - Day 1

- **Describe what an event is, and why it might be useful to a client.**

    - An event is a way to tell the outside world that some action has been done on blockchain. Client can use it on their frontend.

- **Deploy a contract with an event in it, and emit the event somewhere else in the contract indicating that it happened.**

```cadence
pub contract Chapter5 {

    pub event SelectedNumber(number: UInt64)

    pub resource players{
        pub let number:UInt64
        pub let name: String

        init(_number: UInt64, _name: String) {
            self.number = _number
            self.name = _name

            emit SelectedNumber(number: self.number)

        }

    }
}
```
- **Using the contract in step 2), add some pre conditions and post conditions to your contract to get used to writing them out.**

```cadence
pub contract Chapter5 {

    pub event SelectedNumber(number: UInt64)

    pub resource players{
        pub let number:UInt64
        pub let name: String

        init(_number: UInt64, _name: String) {

            pre {
                _name > 0: "not a valid name"
                _number > 0 && _number < 50: "number does not meet the requirements"
            }
            post {
                self.number == _number
                self.name ==_name
            }

            self.number = _number
            self.name = _name

            emit SelectedNumber(number: self.number)

        }

    }
}
```
- **For each of the functions below (numberOne, numberTwo, numberThree), follow the instructions.**

```cadence
pub contract Test {

  // TODO
  // Tell me whether or not this function will log the name.
  // name: 'Jacob'
  pub fun numberOne(name: String) {
    pre {
      name.length == 5: "This name is not cool enough."
    }
    log(name)
  }

  // TODO
  // Tell me whether or not this function will return a value.
  // name: 'Jacob'
  pub fun numberTwo(name: String): String {
    pre {
      name.length >= 0: "You must input a valid name."
    }
    post {
      result == "Jacob Tucker"
    }
    return name.concat(" Tucker")
  }

  pub resource TestResource {
    pub var number: Int

    // TODO
    // Tell me whether or not this function will log the updated number.
    // Also, tell me the value of `self.number` after it's run.
    pub fun numberThree(): Int {
      post {
        before(self.number) == result + 1
      }
      self.number = self.number + 1
      return self.number
    }

    init() {
      self.number = 0
    }

  }

}
```
- **1**:- YES, it will log the name `Jacob` because it's length is 5.

- **2**:- YES, it will return a value `Jacob` and concat it with `Tucker` and also post condition fails.

- **3**:- NO,it will not log the updated number, post condition fails and self.number will be 0
