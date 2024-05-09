https://www.youtube.com/watch?v=7EmboKQH8lM&list=WL&index=3&t=3s&ab_channel=UnityCoin

Bjarne Stroustroup - clean code should do one thing well

A function does one thing if you cannot extract another function from them

1-2 intends in a function

try not more then 3 arguments in the funtion

Avoid bool functions

Avoid output arguments

Avoid switches - use polymorphism (open close principle)

Workaround with side effects using lambdas (and RAII - my comment) - for new/delete, open close

If function returns something - it is does not change the system, if it returns void - it is a command

Dijkstra wanted all the programming to be provable, he found out that some were not (the Halt problem of Turing), and those had hidden GOTO statements. So he wanted to get rid of them. 

Dijkstra failed to prove code - but it is not needed because we could test it.

Comments are often bad - they often lie (over time). Maybe have your comments in red instead of in green in your IDE - to READ them allways
Good comments - explanation / intent / warning
Never check in TODO comments

File size if a style choice - it does not correlate with the size of the project

Name length should be proportional to the size of the variable's scope
The rule is inverted for function and class names - we do not want long names for functions that are called in a lot of places

Tests give your luxury to be not afraid to refactor the code.
So every time you think something could be improved - definitely write a test for it.
Fragile test problem - tests are so coupled so they break when the system changes and when error happens.

Try giving the estimates as thee numbers - good, average and bad

Also tests are the best documentation. They are live examples of all possible use cases of your API

TDD loop:
 - write a failing test before the code
 - write no more code then is needed for a test to succeed
 - write no more test code then is needed for a test to fail

Try mutation test environment! (https://github.com/nlohmann/mutate_cpp)




#clean_code
