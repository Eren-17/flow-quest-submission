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
