# quest-submissions

## Chapter 1 Day 1 Quests

1. The Blockchain a special, secure but open public record of digital items, assets, tools and info that are safely stored in groups that are linked together. Therefore,  everyone knows exactly what the ownership and history is without centralized control or much risk of manipulation.
2. A smart contract is a program with set of rules to infallibly carry out some interaction with a blockchain.
3. A script essentially reads a part of the blockchain. A transaction actually involves a payment but makes some sort of change and addition to the blockchain


## Chapter 1 Day 2 Quests

1. The 5 Pillars of the Cadence smart contract programming language are: safety & security, clarity, approachability, developer experience, and resource oriented programming.
2. Essentially every pillar is in someway related to creating a safe, easy and scalable blockchain smart contract language.


## Chapter 2 Day 1 Quests

1.
![ch2d1-1](https://user-images.githubusercontent.com/106959086/172991959-ff9935fd-7c39-46ee-9826-a23eb5493448.jpg)

```cadence
access(all) contract JacobTucker {

  // Declare a public field of type String.
  // All fields must be initialized in the init() function.
  access(all) let is: String

  // The init() function is required if the contract contains any fields.
  init() {
      self.is = "the best"
  }

}
```


2.
![ch2d1-2](https://user-images.githubusercontent.com/106959086/172991977-7d20d824-83fc-437e-8307-28d222a2cd2e.jpg)

```cadence
import JacobTucker from 0x03

pub fun main(): String {
    return JacobTucker.is
}
```


