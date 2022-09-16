# Goals for this week

- Learn to test-drive programs with multiple classes.
  - [x] Completed Phase 1: Testing Bites
- Learn to break programs up into classes.
- Learn to debug your programs.
- Learn to build software as a pair.
- Learn to explain why test-driving, object-oriented design, debugging, and pairing are powerful practices for software engineers.


# Day 1 Notes

## TDD 
- Write test and then implementation 
- Structure 
- **Mutation testing** - creating mutation for the working code to check that the test is failing

## OOD
Break up programmes into smaller pieces (Classes)

# Day 2 Notes

**Freerunning dev** - doesn't incorporate the tests, can be frustrating when the code becomes complex

## TDD 

- Red phase - just the test
- Green phase - just enough program, so it can behave like the test
- Refactor stage - improve readability, structure
- Repeat the cycle!

## Single-Method Programs Design Recipe

### 1. Describe the Problem
_User story_

### 2. Design the Method Signature
_Include the name of the method(verb), its parameters, return value, and side effects._ 

### 3. Create Examples as Tests
_Make a list of examples of what the method will take and return._
_Encode each example as a test._

### 4. Implement the Behaviour
_After each test, follow the test-driving process of red, green, refactor to implement the behaviour_

## Methodical Debugging

### Change Debugging
- Change the most suspicious part of the code
- Run the code and see if it works\
- Repeat!

### Discovery Debugging
- Investigate how the code executes
  - Control flow
  - Values of variables
- Discover the bug
- Apply change
- Repeat if change is wrong

## Single-Class Program

**Method** - reusable chunk of code, takes argument, returns value.  
**Object** - structure that encapsulates a collection of values ('state'/'memory') and exposes some methods that can operate on that state.  
**Class** - blueprint for creating objects

*In OOP the most important unit of behaviour is the class.*

# Day 3 Notes

## 1. Describe the Problem

_Put or write the user story here. Add any clarifying notes you might have._

## 2. Design the Class Interface

_Include the initializer and public methods with all parameters and return values._

```ruby

class Reminder
  def initialize(name) # name is a string
    # ...
  end

  def remind_me_to(task) # task is a string
    # No return value
  end

  def remind()
    # Throws an exception if no task is set
    # Otherwise, returns a string reminding the user to do the task
  end
end
```

## 3. Create Examples as Tests

_Make a list of examples of how the class will behave in different situations._

```ruby

# 1
reminder = Reminder("Kay")
reminder.remind_me_to("Walk the dog")
reminder.remind() # => "Walk the dog, Kay!"

# 2
reminder = Reminder("Kay")
reminder.remind() # fails with "No task set."

# 3
reminder = Reminder("Kay")
reminder.remind_me_to("")
reminder.remind() # => ", Kay!"
```

_Encode each example as a test. You can add to the above list as you go._

## 4. Implement the Behaviour

_After each test you write, follow the test-driving process of red, green, refactor to implement the behaviour._




