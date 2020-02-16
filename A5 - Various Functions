### Binura Gunasekera
### Assignment 5 Part 1: Functions
### ITI 1120 [D]
### 300021973


### Q1 largest_34(a)
"""
list --> int
Takes list as parameter, and converts to sum of third and fourth largest #'s
Precondition: All elements of list 'a' must be of type(int)
"""

def largest_34(l):
	c=set(l)
	c=list(c)
	return c[-3] + c[-4]


### Q2 largest_third(a)
"""
list --> int
Takes list as parameter, and converts to sum of highest values (in range of len(a)//3)
Precondition: All elements of list 'a' must be of type(int)
"""

def largest_third(a):
    n = len(a)//3
    total = 0
    a.sort(reverse = True)
    for i in range(n):
        total += a[i]
    return total
        

### Q3 third_at_least(a)
"""
list --> int
Takes list as parameter and returns a value that appears ((len(a)//3)+1) times
Precondition: All elements of list 'a' must be of type(int)
"""

def third_at_least(a):
    n = ((len(a))//3)+1
    for i in range(len(a)):
        count = 0
        for k in range(len(a)):
            if a[k] == a[i]:
                count+=1
                if count >= n:
                    return a[i]

### Q4 sum_tri(a,x)
"""
List , int --> bool
Takes as input a list and int, and returns a boolean which depends on whether
or not (a[i] + a[j] + a[k]) == x
Precondition: All elements of list 'a' must be of type(int)
"""

def sum_tri(a,x):
    for i in range(len(a)):
        for j in range(len(a)):
            for k in range(len(a)):
                if (a[i] + a[j] + a[k]) == x:
                    return True
    return False


