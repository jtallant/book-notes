# Clean Code

These are my notes for Clean Code. Some of them won't really make sense without the 
corresponding code example from the book. Be careful when reading these, they are very 
short notes and by nature they lack context. The lack of context can lead to false 
assumptions. They aren't a substitute for the book. I make them to help retain the information.

## Chapter 2 - Meaningful Names

* Use intention revealing names
* Avoid disinformation
    - Don't use var names that already mean something else.
      var pos = "some position related thing". <= bad
* Make meaningful distinctions.
    - Don't use a different spelling just because the name is taken (class vs klass)
* Use pronouncable names
* Use searchable names (single letter names suck)
    - The length of a name should correspond to the size of its scope (think for-loops)
* Avoid encoding names (adding type)
    - Don't put the type in the var name (phoneString)
    - It's okay to encode Interface names but should probably be avoided.
* Avoid mental mapping
    - Don't make people translate some name into something sensible (abbreviations)
      Just use the sensible name.
* Class names
    - Don't use verbs
    - Avoid things like Manager, Info, Data, Processor.
      These do not provide meaning and lead to god objects
    - Customer, WikiPage, AddressParser are examples of good class names
* Don't be cute
    - HolyHandGrenade = delete()
* One word per concept
    - Bad: fetch, get, find are all doing the same thing.
* Don't use the same word for two different ideas. That is a pun.
    - Foo->add() (do addition) vs Foo->add() (array_push())
* Use technical names over domain specific names when possible
    - AccountVisitor signifies the visitor pattern
    - JobQueue is dead obvious
    - Avoid the need for domain knowledge when technical knowledge any programmer
      has will suffice. Programmers will be reading your code, not business people.
* Use problem domain names when programmer-eese names don't make sense
    - The programmer can at least ask a domain expert what it means
* Use namespaces over prefix and suffix
    - Bad: AccountListener
    - Good: Account\Listener\WhenAccountCreated
* Add meaningful context
    - var state vs var addressState
    - An address class would be even better for adding context to the state variable
    - Extract methods and give them meaninful names
* Don't add gratuitous context
    - You have an app called GasStationDeluxe.
      Don't do things like GSDAccountAddress. This goes back to namespaces.
      It should be GasStationDeluxe\Account\Address

## Chapter 3 - Functions
* The first rule of functions is that they should be small.
* The second rule of functions is that they should be smaller than that.
* FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.
    - If a function does only those steps that are one level below the stated name of the
      function, then the function is doing one thing.
    - Another way to know that a function is doing more than “one thing” is if you
      can extract another function from it with a name that is not merely
      a restatement of its implementation. In other words only extract as long
      as you aren't restating the original thing your are doing.
    - Beware of sections within a function (declarations, initializations, and sieve).
      This is a sign of doing more than one thing.
* One level of abstraction per function
    - High level: getHtml()
    - Mid level: PathParser.render(pagePath)
    - Low level: .append()
    - Mixing these levels of abstraction in a single function confuses the reader by
      making essential concepts indistinguishable from minor details.
* Reading code from top to bottom
    - We want every function to be followed by those at the next level of abstraction so
      that we can read the program, descending one level of abstraction at a time as
      we read down the list of functions.
* Switch statements are usually (but not always) a code smell
    - Make sure that each switch statement is buried in a low-level class and
      is never repeated.
    - Often times switch statements signal a design flaw.
    - Indicators of a bad switch statement:
        * Violates the Single Responsibility Principle (more than one reason to change)
        * Violates Open Closed Principle (Must grow as new potential "cases" are added).
        * Other functions rely on the result of the same switch.
    - See if you can bury a switch in an AbstractFactory.
    - General rule for switch statements is that they can be tolerated if they appear
      only once, are used to create polymorphic objects, and are hidden behind an
      inheritance.
* Use descriptive names
    - Don’t be afraid to make a name long. A long descriptive name is better than
      a short enigmatic name
