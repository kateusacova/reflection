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

# Day 4 Notes

```ruby
binding.rb #for debugging
```

Integration test - when testing multiple classes working together. 
Unit test - test for single class. 

Questions for the coach:  
If both methods have the same name (e.g. reading time). How program known which one I want to use?  

## Design a Multi-Class Program

How to figure out how to break out program into classes?
- Emergent Design
  - Start with a single class, and then extract out new classes when it seems like it is doing too much
- Planned Design
  - Design a multi-class system, update each iteration

# Multi-Class Planned Design Recipe

## 1. Describe the Problem

_Put or write the user story here. Add any clarifying notes you might have._

## 2. Design the Class System

_Consider diagramming out the classes and their relationships. Take care to
focus on the details you see as important, not everything. The diagram below
uses asciiflow.com but you could also use excalidraw.com, draw.io, or miro.com_

```
┌────────────────────────────┐
│ MusicPlayer                │
│                            │
│ - add(track)               │
│ - all                      │
│ - search_by_title(keyword) │
│   => [tracks...]           │
└───────────┬────────────────┘
            │
            │ owns a list of
            ▼
┌─────────────────────────┐
│ Track(title, artist)    │
│                         │
│ - title                 │
│ - artist                │
│ - format                │
│   => "TITLE by ARTIST"  │
└─────────────────────────┘
```

_Also design the interface of each class in more detail._

```ruby
class MusicLibrary
  def initialize
    # ...
  end

  def add(track) # track is an instance of Track
    # Track gets added to the library
    # Returns nothing
  end

  def all
    # Returns a list of track objects
  end
  
  def search_by_title(keyword) # keyword is a string
    # Returns a list of tracks with titles that include the keyword
  end
end

class Track
  def initialize(title, artist) # title and artist are both strings
  end

  def format
    # Returns a string of the form "TITLE by ARTIST"
  end
end
```

## 3. Create Examples as Integration Tests

_Create examples of the classes being used together in different situations and
combinations that reflect the ways in which the system will be used._

```ruby
# EXAMPLE

# Gets all tracks
library = MusicLibrary.new
track_1 = Track.new("Carte Blanche", "Veracocha")
track_2 = Track.new("Synaesthesia", "The Thrillseekers")
library.add(track_1)
library.add(track_2)
library.all # => [track_1, track_2]
```

## 4. Create Examples as Unit Tests

_Create examples, where appropriate, of the behaviour of each relevant class at
a more granular level of detail._

```ruby
# EXAMPLE

# Constructs a track
track = Track.new("Carte Blanche", "Veracocha")
track.title # => "Carte Blanche"
```

_Encode each example as a test. You can add to the above list as you go._

## 5. Implement the Behaviour

_After each test you write, follow the test-driving process of red, green,
refactor to implement the behaviour._


# Mocking bites

Instead of using real class instances (e.g. DairyEntry for Dairy), we use fake instances (doubles), so that we can test the parent Class withour relying on its child class.

``` ruby
fake_diary_entry_1 = double :diary_entry # just the empty class

fake_diary_entry_1 = double :diary_entry, count_words: 2 # class with methodss
```
