## Chapter 4 - Day 3

- **Q.1 Why did we add a Collection to this contract? List the two main reasons.**

    - We added a collection to this contract, because if not we would have to store each NFT at different path and remember every path.

    - To allow others to be able to mint or deposit NFTs for us. We added a collection.

- **Q.2 What do you have to do if you have resources "nested" inside of another resource? ("Nested resources")**

    - We need to make use of `destroy` keyboard. And **destroy** the nested resource.

- **Q.3 Brainstorm some extra things we may want to add to this contract. Think about what might be problematic with this contract and how we could fix it.**

 - ***Idea #1: Do we really want everyone to be able to mint an NFT? 🤔.***

    - No, this will lead to users minting as many NFTs they want. We could use resource interface and allow only the selected users to mint the NFTs.

 - ***Idea #2: If we want to read information about our NFTs inside our Collection, right now we have to take it out of the Collection to do so. Is this good?***

    - No, moving a resource just to read is not a good idea. Instead just get the reference or use `.borrow()`.
