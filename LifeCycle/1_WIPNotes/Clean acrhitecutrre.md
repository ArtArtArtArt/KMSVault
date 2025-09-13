https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html?utm_source=pocket_mylist

#programming/architecutre
# Clean acrhitecutrre
![[Pasted image 20220311111459.png]]

Main rule is that dependencies may only point inwards.
## Circles

### Entities
Are business rules and business objects

### Use cases
Application specific rules. The flow of data.

### Interface adapters
Convert data from usecases and entities to external agency (Database, Web). [[Persistence framework]]

### Frameworks and Drivers
The outside user of the system


There might be more circles but the Dependency rule should be the same.

*this all looks very familiar to [[layered architecture]]. I have a hypothesis that this is the same approach*

## Crossing the boundaries

MIght sometime be needed. The [[dependancy inversion]] principle should be used here.

## What data should be 

Data should be wrapped in simple data structures. They also should be the most convenient for the inner circle because otherwise the dependency principle will be broken (inner circle will know some names from the outer circles)/