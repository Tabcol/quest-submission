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

## Chapter 2, Day 2 Quests

1. We would not call changeGreeting in a script because changeGreeting is a function in the execute phase of a transaction. A script only reads and returns information on the blockchain.
2. In the prepare phase of a transaction AuthAcct gives the ability to read the data in the account; and that is taken in once the user pays for and signs/approves a transaction.
3. The prepare phase is used to get the information and data of the user/signer's account, via AuthAcct (which can only be used in the prepare phase). Changes can also be made in the prepare phase, but that is not a good practice as can make things less clear. The execute phase of the transaction is where changes to the blockchain should be made/executed if rules of the smart contract are met. 
4. 
![ch2d4-1](https://user-images.githubusercontent.com/106959086/173254769-bcc16a2d-5167-46f2-91db-4e555b647d3e.jpg)
```cadence
pub contract HelloWorld {

    pub var greeting: String
    pub var myNumber: Int

    pub fun changeGreeting(newGreeting: String) {
        self.greeting = newGreeting
    }
  
    pub fun updateMyNumber(newNumber: Int){
        self.myNumber = newNumber
    }

    init() {
        self.greeting = "Hello, World!"
        self.myNumber = 0
    }

}
```

wanted to do a script that passed in the int and string but know I need a different structure for that.

![ch2d4-2](https://user-images.githubusercontent.com/106959086/173254856-80f6a922-54a4-4012-94ef-5dc6b4824883.jpg)

```cadence
import HelloWorld from 0x01

pub fun main(): Int {
        return HelloWorld.myNumber
}
```
Executed transaction to change number (did not display anything in results in playground)
![ch2d4-3](https://user-images.githubusercontent.com/106959086/173255144-bf506b7d-5261-4390-8725-a0b7c9fe4927.jpg)

```cadence
import HelloWorld from 0x01

transaction(myNewNumber: Int) {

  prepare(signer: AuthAccount) {}

  execute {
    HelloWorld.updateMyNumber(newNumber: myNewNumber)
  }
}
```

Ran script again to confirm successfully changed number
![ch2d4-4](https://user-images.githubusercontent.com/106959086/173255227-e15fa432-730c-4005-9191-224ad0f11262.jpg)


## Chapter 2, Day 3 Quest
 1.
 ![ch2d3-1](https://user-images.githubusercontent.com/106959086/173716273-a88f0a5d-5862-4fbc-b80e-5401a1f1b7e1.jpg)
 
 ```cadence
pub fun main() 
{
    var s: [String] = ["T-Bone", "Coco Rico", "A Dawgs"]
    log(s)
}
 ```
 
 2.
 ![ch2d3-2](https://user-images.githubusercontent.com/106959086/173738308-4983b917-16a6-4e08-b0e8-29e12028d492.jpg)

```cadence
pub fun main() 
{
    // 1. with variable changed to "S"
    var S: [String] = ["T-Bone", "Coco Rico", "A Dawgs"]
    log(S)

    // 2.
    var s: {String: Int} = {"Facebook": 3, "Instagram": 1, "Twitter": 4, "YouTube": 5, "Reddit": 2, "LinkedIn": 0}
    log(s)
}
```

3. Dictionaries when accessed by a function return an optional value ```? ``` as either the return type (String, Int, or Address) or returns null/nil/void if there is no key, value or index or unexpected variable. We can use the force unwrap opperator ```!``` to remove/force unwrap the optional. The panic feature ```?? panic("Not today boo")``` can also by used as an alternative to more specifically locate where an error occured. Anothere option is to make the return type of the function optional

I added this code to the script and ran - retured void...
```cadence
  //3. 
    pub fun main2(): Address?
{ 
    let peeps: {Int: Address} = {1: 0x01, 2: 0x02, 3: 0x03}
    return peeps [1]
}
```
to use the unwrap opperator I changed to this, ran script and took screen shot:)
```cadence
  //3. 
    pub fun main2(): Address 
{ 
    let peeps: {Int: Address} = {1: 0x01, 2: 0x02, 3: 0x03}
    return peeps [1]! 
}
```
![ch2d3-3](https://user-images.githubusercontent.com/106959086/173785677-2495c5c1-b5b5-4d37-8b7c-c1272de75c06.jpg)

4. It means we messed up doing something with a dictionary most likely. The function calling the dictionary returns a optional value ```String?``` therefore doesn't match unwrappped value type stored in dictionary ```String``` so returns this mismatched type error.
   To fix we can make String optional ```pub fun main (): String? {```
   Or leave ```String``` in that first line and add unwrap opperation to end of line 3: ```return thing[0x03]!```
   A 3rd option is to add panic option to that line: ```return thing[0x03]?? panic("Error Returning thing value")```


## Chapter 2, Day 4

Contract: 
```cadence
pub contract GoldenIdolsQuest {

    pub var teams: {Int: Teams}
    
    pub struct Teams {
        pub let flovs: String
        pub let points: Int
        pub let place: Int

        init(_flovs: String, _points: Int, _place: Int) {
            self.flovs = _flovs
            self.points = _points
            self.place = _place
           
        }
    }

    pub fun addTeam(flovs: String, points: Int, place: Int) {
        let newTeam = Teams(_flovs: flovs, _points: points, _place: place)
        self.teams[place] = newTeam
    }

    init() {
        self.teams = {}
    }

}
```
Transaction:
![ch2d4-a](https://user-images.githubusercontent.com/106959086/174385778-b6d6a502-791d-4ac3-8451-d71fe62ac994.jpg)

```cadence
import GoldenIdolsQuest from 0x01

transaction(flovs: String, points: Int, place: Int) {

    prepare(signer: AuthAccount) {}

    execute {
        GoldenIdolsQuest.addTeam(flovs: flovs, points: points, place: place)
        log("Droids Rule Flovatar;)")
    }
}
```
![ch2d4-b](https://user-images.githubusercontent.com/106959086/174458548-2beb14b2-bacd-40c2-97f6-9e11d6ab3e24.jpg)

Script:
```cadence
import GoldenIdolsQuest from 0x01

pub fun main(place: Int): GoldenIdolsQuest.Teams {
    return GoldenIdolsQuest.teams[place]!
}
```

## Chapter 3, Day 1

1. Structs look similar but are very different from resources. Structs can be created from outside of a contract, resources can not. Structs can be copied, resources can only be ```<-``` moved. Structs are less complicated than resources because the rules for handling and interacting with the later. Resources can be burned but they can't be lost or comprimised by overwrite.
2. A resource would be needed over a struct whenever storing something of value such as an NFT or token.
3. ```create``` is they keyword required, in the contract, that is used to make a resource.
4. A resource can only be created within a contract, not a transaction or script.
5. Jacob is a public type resouce here:
```cadence
 pub resource Jacob{
 
 }
 ```

6.
![ch2d4-c](https://user-images.githubusercontent.com/106959086/174504763-76bfccb9-86c3-4325-979a-3f10a8e026c9.jpg)

```cadence
pub contract Test {

    // Hint: There's nothing wrong here ;)
    pub resource Jacob {
        pub let rocks: Bool
        init() {
            self.rocks = true
        }
    }

    pub fun createJacob(): @Jacob {  // added @ to resource
        let myJacob <- create Jacob() // changed to <- and added create
        return <- myJacob // again changed = to <-
    }
 }
 ```

