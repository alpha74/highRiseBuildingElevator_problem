# High Rise Building Elevator Problem

### Problem Statement
Consider a high rise building having floors >= 200. We have to design an algorithm for `elevator` system.

Given the number of lifts as N and M people are requesting the lifts rapidly.

Design an algorithm which would solve these problems:
- Minimise the wait time for each lift.
- In morning, a lot of people will be going to their offices. Hence, load would be high between 8-9am.
- In evening, a lot of people would be going down so load will be high but it will be random.
- Avoid the situation when a lift arrives and it is full.

-----


### Analysis

We try to analyze the problem taking some assumptions about the amount of people working in the building.

:white_check_mark: **Taking an example:**
- The building has 200 floors ( Let `F` be number of floors )
- Lift capacity `C`
- A total of 100 people work on each floor ( Let `W` be number of people working on each floor. It can be range of numbers. )
- Total people visiting the building = 200 x 100 = 2000 (+- 200 others ) ( Denoted by `F.W` )

:white_check_mark: **In this example, we notice that:**
- The people only go the floors which they work on, i.e, a person who works on floor 10 will not go (or rarely) go above floor 10.
- The above condition is valid for every person with respect to their `work_floor`.
- We use this insight to design the elevator system.


:white_check_mark: **Insights for lift system:**
- The traffic load on lifts will be highest for `floor 1` and lowest for `floor F` : How?
  - Number of people travelling in lifts from `floor 0` to `floor 1` will include all the people wanting to go up any floor.

- The lower floors will have high movement of people as compared to topmost floors. 
- We use this insight in our lift system. 
  - Lower floors have more lifts as compared to upper floors.
  
  
-----
  
### Solution:

- `N` is the number of lifts.
- We divide the number of lifts in decreasing order from bottom to top.
- Each lift is deployed only for a specific floor_range (Eg: floor10-15). Hence, there exists no lift which goes from `floor 0` to `floor f`.
- `list_lifts` holds number of lifts which are to be deployed in the decreasing order.
- `threshold` denotes the minimum number of lifts for deployment across a floor range.
- `div_factor` denotes the amount of distribution needed. It depends on `N` and `M`, and is hard coded here.
- `inc_factor` denotes increase in `div_factor`.

```
list_lifts = []
div_factor = 3
inc_factor = 2
threshold = 5
N = number of lifts
tempN = N

bool stop = false

while( !stop )
{
  N = N / div_factor
  
  if( N >= threshold )
    list_lifts.append( N )
  else
    list_lifts.append( tempN - N )
    
  div_factor += inc_factor
}

sort_desc( list_lifts )
```

### Example:

- `N = 50`
- `F = 200`
- `C = 30`
- `list_lifts` : `[16, 12, 10, 7, 5 ]`
- We divide these number of lifts across the floor range 0-50. 
- The lifts groups are discontinuous:
  - People will have to get out after reaching the topmost floor a lift can go.
  - And board one of the lift in next group of lifts.
  
- Here, number of groups = `list_lifts.size() = 5`. We deploy lifts like this:
  - `floor 0-10` : 16 lifts running in parallel. This floor range has largest number of lifts as it has most traffic movement.
  - `floor 11-20` : 12 lifts running in parallel. This group of lifts is separate from all others.
  - `floor 21-30` : 10 lifts running in parallel. This group of lifts is separate from all others.
  - `floor 31-40` : 7 lifts running in parallel. This group of lifts is separate from all others.
  - `floor 41-50` : 5 lifts running in parallel. This group of lifts is separate from all others.


### Example Diagram
![Example_Diagram](https://github.com/alpha74/highRiseBuildingElevator_problem/blob/master/assets/diag1.jpg)

-----


### Improvement
- A more smooth distribution function can be used which depends on more parameters like actual number of people in each floor.
- This will lead to more efficient distribution of number of lifts.
