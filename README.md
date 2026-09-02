**QUESTION**
University Timetable
A university needs to assign subjects to classrooms and time slots while avoiding conflicts between subjects and teachers.
Question: How can backtracking be applied to find a valid timetable? 


**SOLUTION**

# University Timetable Using Backtracking

## 1. Description

Backtracking is an algorithm used to find a valid solution by trying different choices.

For a university timetable:

* We assign a subject to a **time slot** and **classroom**.
* We check whether there is a conflict.
* If there is no conflict, we continue with the next subject.
* If we reach a problem, we **go back** and try another choice.

The main idea is:

**Choose → Check → Assign → Continue → If wrong, go back → Try again**

## 2. Example

Suppose a university has:

### Subjects

* Python → Teacher T1
* DBMS → Teacher T2
* Networks → Teacher T1

### Classrooms

* R1
* R2

### Time Slots

* 9AM
* 10AM
* 11AM

A possible valid timetable is:

| Subject  | Time | Room | Teacher |
| -------- | ---- | ---- | ------- |
| Python   | 9AM  | R1   | T1      |
| DBMS     | 9AM  | R2   | T2      |
| Networks | 10AM | R1   | T1      |

### How backtracking works

1. Python is assigned to **9AM, R1**.
2. DBMS tries **9AM, R1**.
3. R1 is already occupied at 9AM, so there is a conflict.
4. Backtracking tries **9AM, R2**.
5. DBMS is assigned to R2.
6. Networks tries available rooms and slots.
7. It gets **10AM, R1** because teacher T1 is free at 10AM.
8. All subjects are assigned successfully.

## 3. Algorithm

1. Start with an empty timetable.
2. Select the next subject.
3. Select a time slot.
4. Select a classroom.
5. Check whether the classroom is already occupied at that time.
6. Check whether the teacher is already teaching at that time.
7. If there is no conflict, assign the subject.
8. Move to the next subject.
9. If the next subject cannot be assigned, remove the previous assignment.
10. Try another room or time slot.
11. Continue until all subjects are assigned.
12. If all subjects are assigned, the timetable is valid.

**Python Implementation**

# List of subjects 
subjects = ["Python", "DBMS", "Networks"] 
 
# Teacher for each subject 
teachers = ["T1", "T2", "T1"] 
 
# List of classrooms 
rooms = ["R1", "R2"] 
 
# List of time slots 
slots = ["9AM", "10AM", "11AM"] 
 
# Empty timetable 
schedule = [] 
 
# Function to assign subjects 
def assign(subjects, rooms, slots): 
 
    # If all subjects are assigned 
    if not subjects: 
        return True 
 
    # Select the first subject 
    subject = subjects[0] 
 
    # Get the teacher of the subject 
    teacher = teachers[len(schedule)] 
 
    # Start checking time slots 
    s = 0 
 
    while s < len(slots): 
 
        # Start checking rooms 
        r = 0 
 
        while r < len(rooms): 
 
            # Select current slot and room 
            slot = slots[s] 
            room = rooms[r] 
 
            # Assume there is no conflict 
            ok = True 
 
            # Check previous assignments 
            i = 0 
 
            while i < len(schedule): 
 
                # Check room conflict 
                if schedule[i][1] == slot and schedule[i][2] == room: 
                    ok = False 
 
                # Check teacher conflict 
                if schedule[i][1] == slot and schedule[i][3] == teacher: 
                    ok = False 
 
                i += 1 
 
            # If there is no conflict 
            if ok: 
 
                # Add subject to timetable 
                schedule.append([subject, slot, room, teacher]) 
 
                # Assign the next subject 
                if assign(subjects[1:], rooms, slots): 
                    return True 
 
                # Backtrack 
                schedule.pop() 
 
            # Try next room 
            r += 1 
 
        # Try next time slot 
        s += 1 
 
    # No valid assignment 
    return False 
 
 
# Start the assignment 
if assign(subjects, rooms, slots): 
 
    # Print the timetable 
    print(schedule) 
 
else: 
 
    # Print if no timetable is possible 
    print("No solution")
```
**
## 5. Time Complexity**

Let:

* **N** = number of subjects
* **T** = number of time slots
* **R** = number of rooms

For every subject, we can try:

T × R

possible combinations.

So the worst-case time complexity is:

**O(N × (T × R)^N)**

because we store the timetable and recursion information for the subjects

## Quick Exam Point

### Backtracking

**Backtracking means trying a choice, and if it does not work, going back and trying another choice.**

### Remember:

**Choose → Check → Assign → Continue → Backtrack → Try Again**
