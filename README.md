# High Rise Building Elevator Problem

### Problem Statement
Consider a high rise building having floors >= 200. We have to design an algorithm for `elevator` system.

Given the number of lifts as N and M people are requesting the lifts rapidly.

Design an algorithm which would solve these problems:
- Minimise the wait time for each lift.
- In morning, a lot of people will be going to theie offices. Hence, load would be high between 8-9am.
- In evening, a lot of people would be going down so load will be high but it will be random.
- Avoid the situation when a lift arrives and it is full.

-----


### Analysis

We try to analyze the problem taking some assumptions about the amount of people working in the building.
Taking an example:
- The building has 200 floors.
- A total of 100 people work on each floor.
- Total people visiting the building = 200 x 100 = 2000 (+- 200 others )

In this example, we notice that:
- The people only go the floors which they work on, i.e, a person who works on floor 10 will not go (or rarely) go above floor 10.
- The above condition is valid for every person with respect to their `work_floor`.
- We use this insight to design the elevator system.
