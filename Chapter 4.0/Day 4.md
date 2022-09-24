## Chapter 4 - Day 4

- **Q.1 Take our NFT contract so far and add comments to every single resource or function explaining what it's doing in your own words.**

``` cadence
pub contract CryptoPoops {
  pub var totalSupply: UInt64

  // This is an NFT resource that contains a name,
  // favouriteFood, and luckyNumber
  pub resource NFT {
    pub let id: UInt64

    pub let name: String
    pub let favouriteFood: String
    pub let luckyNumber: Int

    init(_name: String, _favouriteFood: String, _luckyNumber: Int) {
      self.id = self.uuid

      self.name = _name
      self.favouriteFood = _favouriteFood
      self.luckyNumber = _luckyNumber
    }
  }

  // This is a resource interface that allows us to.
  // Deposit or add NFTs, with the deposit() fun below.
  // Get the list of NFTs Id, with the getIds() fun below.
  // Get reference to our NFT, with the borrowNFT() fun below.
  pub resource interface CollectionPublic {
    pub fun deposit(token: @NFT)
    pub fun getIDs(): [UInt64]
    pub fun borrowNFT(id: UInt64): &NFT
  }

  // This resource "Collection" is implementing the above resource interface "CollectionPublic"
  // But it also includes,
  // a dictionary "ownedNFTs" which maps UInt64 to the NFT resource above.
  // a withdraw fun to withdraw NFTs.
  pub resource Collection: CollectionPublic {
    pub var ownedNFTs: @{UInt64: NFT}

    // fun to add or deposit NFTs in the collection.
    pub fun deposit(token: @NFT) {
      self.ownedNFTs[token.id] <-! token
    }

    // fun to withdraw NFTs from the collection and return it.
    pub fun withdraw(withdrawID: UInt64): @NFT {
      let nft <- self.ownedNFTs.remove(key: withdrawID) 
              ?? panic("This NFT does not exist in this Collection.")
      return <- nft
    }

    // fun to get the list of Ids available inside the collection.
    pub fun getIDs(): [UInt64] {
      return self.ownedNFTs.keys
    }

    // fun to get the reference for an NFT, using it's Id
    pub fun borrowNFT(id: UInt64): &NFT {
      return (&self.ownedNFTs[id] as &NFT?)!
    }

    // initializing a empty "ownedNFTs" dictionary at the time of contract deployment.
    init() {
      self.ownedNFTs <- {}
    }

    // We are destroying the "ownedNFTs"
    destroy() {
      destroy self.ownedNFTs
    }
  }

  // creating an empty collection having a Collection resource type.
  pub fun createEmptyCollection(): @Collection {
    return <- create Collection()
  }

  // A resource that allows the OWNER to mint the NFTs 
  pub resource Minter {

    // creating NFT with some parameters
    pub fun createNFT(name: String, favouriteFood: String, luckyNumber: Int): @NFT {
      return <- create NFT(_name: name, _favouriteFood: favouriteFood, _luckyNumber: luckyNumber)
    }

    // fun to create minter,
    // basically it allows us to change the minter
    pub fun createMinter(): @Minter {
      return <- create Minter()
    }

  }

  init() {
    // initializing the totalsupply to be zero, before a NFT is minted. 
    self.totalSupply = 0
    // Save the `Minter` resource to account storage 
    // this way the signer becomes the owner of the Minter resource and can MINT NFTs.
    self.account.save(<- create Minter(), to: /storage/Minter)
  }
}
```
