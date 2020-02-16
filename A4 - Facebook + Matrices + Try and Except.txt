### Assignment 4: Matrices
### 300021973
### ITI 1120 [D]
### Binura Gunasekera

import random

def create_network(file_name):
    '''(str)->list of tuples where each tuple has 2 elements the first is int and the second is list of int

    Precondition: file_name has data on social netowrk. In particular:
    The first line in the file contains the number of users in the social network
    Each line that follows has two numbers. The first is a user ID (int) in the social network,
    the second is the ID of his/her friend.
    The friendship is only listed once with the user ID always being smaller than friend ID.
    For example, if 7 and 50 are friends there is a line in the file with 7 50 entry, but there is line 50 7.
    There is no user without a friend
    Users sorted by ID, friends of each user are sorted by ID
    Returns the 2D list representing the frendship nework as described above
    where the network is sorted by the ID and each list of int (in a tuple) is sorted (i.e. each list of friens is sorted).
    '''
    friends = open(file_name).read().splitlines()
    network=[]

    # YOUR CODE GOES HERE
    
    ### PLEASE NOTE THAT ALL THE FOLLOWING CODE IS PART OF ONE FUNCTION ("create_network(file_name)")
    ### Individual docstrings are given to each set of loops to explain what it does


    ### Starter variables required to complete the friend organization process
    friends.pop(0) # removes first line of the .txt file
    sortednetwork = [] # 3 blank lists to store different items created throughout the loops
    checklist = []
    finalList = []


    """
    (str --> list(list of str) (matrix with list of strings) Makes a matrix in the form [['a','x'],['b','y']]
    Takes string data from file_name and then converts it to list(list of str)
    Precondition: friends(the data from the file) must contain data, and that too must be numerical data
    """


    
    for i in friends:
        i = i.split(" ")
        
        network.append(i)
    """
    list(list of str) --> list(list of int) Makes a matrix in the form of [[a,x],[b,y]]
    Takes string list (network) and converts it to int
    Precondition: all elements of network must be of type (int)
    """


    
    for i in range(len(network)):
        for k in range(len(network[0])):
            network[i][k] = int(network[i][k])
    """
    (list(list of str)) --> (list of int), Makes a list in the form [a,b,c,d,e]
    Takes all elements of matrice "network" of column[0], and adds it into list of int (creates unique list of int containing all ID's in column[0]
    Precondition: all elements of network[i][0] must be of type int
    """

    
    
    for i in range(len(network)):
        if network[i-1][0] != network[i][0] :
            sortednetwork.append([network[i][0]])
    """
    empty list --> (list of int), Makes a list of the form [a,b,c,d,e,f]
    Takes all elements of column[0] of sortednetwork, and adds it to blanklist "checklist"
    Precondition: sortednetwork must have at least 1 element of type (any)
    """
    

    
    for i in range(len(sortednetwork)):
        checklist.append(sortednetwork[i][0])
    
    """
    (list of int) --> (list of int) Makes a list of the form [a,b,c,d,e,f,f,g,g]
    Takes all elements of checklist, and adds all elements of network[row][1] that aren't already present
    This essentially adds all the ID's of individuals in the friend network into a list, and sorts them by Lowest --> Highest
    Precondition: None
    """



    
    for row in range(len(network)):
        if network[row][1] not in checklist:
            sortednetwork.append([network[row][1]])
            sortednetwork = sorted(sortednetwork)
    """
    (list of int) --> list(list of int) Makes a matrix of the form [[a],[b],[c],[d],[e],[f],[g],[],[]]
    Removes all duplicate items present in sortednetwork (namely the newly added elements in the previous loop)
    The removed items leave behind [] since del list method is used
    Precondition: None
    """
    


    for row in range(len(sortednetwork)-1):
        if sortednetwork[row][0] == sortednetwork[row+1][0]:
            del[sortednetwork[row][0]]
    """
    list(list of int) --> list(list of int) Makes a matrix of the form [[a],[b],[c],[d],[e],[f]]
    Removes all empty brackets left behind by the del list method from the above loop
    Precondition: None
    """



    while [] in sortednetwork:
        sortednetwork.remove([])
    """
    list(list of int) --> list(list(list of int)) Makes a triple layered matrix of the form [[a,[b,c,d]],[f,[g,h,j]]]
    Adds all the friends of the user ID into a empty list (Z) and then list Z is appended to sortednetwork
    However no friends of lesser ID are added (another loop is required)
    Precondition: None
    """



    for i in range(len(sortednetwork)):
        Z=[]
        for a in range(len(network)):
            if sortednetwork[i][0] == network[a][0]:
                Z.append(network[a][1])
        sortednetwork[i].append(Z)
    """
    list(list(list of int)) Makes a triple layered matrix of the form [[a,[b,c,d,e]],[f,[g,h,j,k]]]
    Adds all friends of lesser ID to sortednetwork via list method .extend
    All friends of lesser ID are added to empty list (R) which is appended to sortednetwork
    Precondition: None
    """


    
    for i in range(len(sortednetwork)):
        R=[]
        for a in range(len(network)):
            if (sortednetwork[i][0] == network[a][1]):
                R.append(network[a][0])
        sortednetwork[i][1].extend(R)   
    """
    list(list(list of int)) Makes a sorted triple layered matrix of the form [[a,[b,c,d,e]],[f,[g,h,j,k]]]
    Sorts sortednetwork completely (the friend list, and the IDs)
    Precondition: All elements of sortednetwork are of type(int) 
    """


    
    for i in range(len(sortednetwork)):
        sortednetwork[i][1].sort()
        sortednetwork.sort()
    """
    list(tuple(list of int)) Makes a sorted triple layered matrix of the form [(a,[b,c,d]),(b,[f,g,h])]
    Converts each ID and it's respective list of friends into type(tuple) and then appends to empty list "finalList"
    finalList is then set equal to network, and network is returned
    Precondition: sortednetwork contains elements of type(any)
    """


    
    for i in range(len(sortednetwork)):
        i = tuple(sortednetwork[i])
        finalList.append(i)
        network = finalList
    
    return network


##############################################################################
    
def getCommonFriends(user1, user2, network):
    '''(int, int, 2D list) ->int
    Precondition: user1 and user2 IDs in the network. 2D list sorted by the IDs, 
    and friends of user 1 and user 2 sorted 
    Given a 2D-list for friendship network, returns the sorted list of common friends of user1 and user2
    '''
    common=[]
    
    # YOUR CODE GOES HERE

    friends2 = open(file_name).read().splitlines()
    friends2.pop(0)
    friends2 = list(friends2)
    newL = []
    friend1 = []
    friend2 = []
    
    
    for i in friends2:
        i = i.split(" ")
        friends2 = i[0].strip()
        newL.append(i)
    
        
   
    for i in range(len(newL)):
        for j in range(len(newL[0])):
            newL[i][j] = int(newL[i][j])
    
    
        
    # Makes list of friends of user1
    for i in range(len(newL)):
        for j in range(len(newL[0])):
            if (newL[i][j-1] == user1) or (newL[i][j] == user1):
                if newL[i][j-1] == user1:
                    if newL[i][j] not in friend1:
                        friend1.append(newL[i][j])
                    
                elif newL[i][j] == user1:
                    if newL[i][j] == user1:
                        if newL[i][j-1] not in friend1:  
                            friend1.append(newL[i][j-1])
    

    # Makes list of friends of user2
    for i in range(len(newL)):
        for j in range(len(newL[0])):
            if (newL[i][j-1] == user2) or (newL[i][j] == user2):
                if newL[i][j-1] == user2:
                    if newL[i][j] not in friend2:
                        friend2.append(newL[i][j])
                    
                elif newL[i][j] == user2:
                    if newL[i][j] == user2:
                        if newL[i][j-1] not in friend2:  
                            friend2.append(newL[i][j-1])
    
    # Checks if elements (one by one) of list(friend1) in friend2, and if it is, it appends to common
    for i in range(len(friend1)):
        if friend1[i] in friend2:
            common.append(friend1[i])
        else:
            continue
    common = sorted(common)
    
    return common


###############################################################################

def recommend(user, network):
    '''(int, 2Dlist)->int or None
    Given a 2D-list for friendship network, returns None if there is no other person
    who has at least one neighbour in common with the given user and who the user does
    not know already.
    
    Otherwise it returns the ID of the recommended friend. A recommended friend is a person
    you are not already friends with and with whom you have the most friends in common in the whole network.
    If there is more than one person with whom you have the maximum number of friends in common
    return the one with the smallest ID. '''

    # YOUR CODE GOES HERE

    
    friends3 = open(file_name).read().splitlines()
    friends3.pop(0)
    friends3 = list(friends3)
    newerL = []
    userfriend = []
    notfriend = []
    x = []
    
    
    
    for i in friends3:
        i = i.split(" ")
        friends3 = i[0].strip()
        newerL.append(i)
    
        
   
    for i in range(len(newerL)):
        for j in range(len(newerL[0])):
            newerL[i][j] = int(newerL[i][j])
    

    for i in range(len(newerL)):
        for j in range(len(newerL[0])):
            if (newerL[i][j-1] == user) or (newerL[i][j] == user):
                if newerL[i][j-1] == user:
                    if newerL[i][j] not in userfriend:
                        userfriend.append(newerL[i][j])
                else:
                    if newerL[i][j-1] not in userfriend:
                        userfriend.append(newerL[i][j-1])
    
   
    for i in range(len(newerL)):
        for j in range(len(newerL[0])):
            if (newerL[i][j-1] not in userfriend) or (newerL[i][j] not in userfriend):
                if newerL[i][j-1] not in userfriend:
                    if newerL[i][j-1] not in notfriend and (newerL[i][j-1] != user):
                        notfriend.append(newerL[i][j-1])
                    else:
                        continue
                if newerL[i][j] not in userfriend:
                    if newerL[i][j] not in notfriend and (newerL[i][j] != user):
                        notfriend.append(newerL[i][j])
                    else:
                        continue
            else:
                continue
    notfriend = sorted(notfriend)
            
    
    for i in range(len(notfriend)):
        x.insert(i,[notfriend[i],getCommonFriends(notfriend[i],user,newerL)])

        
    highest = 0
    recommended = None
    for i in range(len(x)):
        if len(x[i][1])>highest:
            highest = len(x[i][1])
            recommended = x[i][0]
        else:
            continue
    return recommended
    


#############################################################################
    
def k_or_more_friends(network, k):
    '''(2Dlist,int)->int
    Given a 2D-list for friendship network and non-negative integer k,
    returns the number of users who have at least k friends in the network
    Precondition: k is non-negative'''
    # YOUR CODE GOES HERE

    
    total = 0
    totalLengths = []
    for i in range(len(network)):
        totalLengths.append(len(network[i][1]))
        if (len(network[i][1])) >= k:
            total+=1
    return total

 

##############################################################################

def maximum_num_friends(network):
    '''(2Dlist)->int
    Given a 2D-list for friendship network,
    returns the maximum number of friends any user in the network has.
    '''
    # YOUR CODE GOES HERE

    
    allLengths = []
    for i in range(len(network)):
        allLengths.append(len(network[i][1]))
    return max(tuple(allLengths))
    
    pass
    


##############################################################################

def people_with_most_friends(network):
    '''(2Dlist)->1D list
    Given a 2D-list for friendship network, returns a list of people (IDs) who have the most friends in network.'''
    max_friends=[]
    # YOUR CODE GOES HERE
    
    callmax = maximum_num_friends(network)
    
    
    for i in range(len(network)):
        if len(network[i][1]) >= callmax:
            max_friends.append(network[i][0])
              
    return    max_friends
    


##############################################################################


def average_num_friends(network):
    '''(2Dlist)->number
    Returns an average number of friends overs all users in the network'''

    # YOUR CODE GOES HERE

    total = 0
    finalsum = len(network)
    for i in range(len(network)):
        total+= len(network[i][1])
    return (total/finalsum)
    
    
    pass


##############################################################################    

def knows_everyone(network):
    '''(2Dlist)->bool
    Given a 2D-list for friendship network,
    returns True if there is a user in the network who knows everyone
    and False otherwise'''
    
    # YOUR CODE GOES HERE
    
    
    for i in range(len(network)):
        if len(network[i][1]) == (len(network)-1):
            return True
        
    return False
    
    pass



###############################################################################

####### CHATTING WITH USER CODE:

def is_valid_file_name():
    '''None->str or None'''
    file_name = None
    try:
        file_name=input("Enter the name of the file: ").strip()
        f=open(file_name)
        f.close()
    except FileNotFoundError:
        print("There is no file with that name. Try again.")
        file_name=None
    return file_name 

def get_file_name():
    '''()->str
    Keeps on asking for a file name that exists in the current folder,
    until it succeeds in getting a valid file name.
    Once it succeeds, it returns a string containing that file name'''
    file_name=None
    while file_name==None:
        file_name=is_valid_file_name()
    return file_name


###############################################################################

def get_uid(network):
    '''(2Dlist)->int
    Keeps on asking for a user ID that exists in the network
    until it succeeds. Then it returns it'''
    
    # YOUR CODE GOES HERE
        
    while True:
        try:
            x = int(input("Please enter an integer for a user ID: "))
            if int(x)==x:
                for i in range(len(network)):
                    if x == network[i][0]:
                        return x
                    else:
                        False
        except NameError:
            print("That was not an integer input, please try again")
        except ValueError:
            print("That was not an integer input, please try again")
        
    pass
    

##############################
# main
##############################

# NOTHING FOLLOWING THIS LINE CAN BE REMOVED or MODIFIED

file_name=get_file_name()
    
net=create_network(file_name)

print("\nFirst general statistics about the social network:\n")

print("This social network has", len(net), "people/users.")
print("In this social network the maximum number of friends that any one person has is "+str(maximum_num_friends(net))+".")
print("The average number of friends is "+str(average_num_friends(net))+".")
mf=people_with_most_friends(net)
print("There are", len(mf), "people with "+str(maximum_num_friends(net))+" friends and here are their IDs:", end=" ")
for item in mf:
    print(item, end=" ")

print("\n\nI now pick a number at random.", end=" ")
k=random.randint(0,len(net)//4)
print("\nThat number is: "+str(k)+". Let's see how many people has that many friends.")
print("There is", k_or_more_friends(net,k), "people with", k, "or more friends")

if knows_everyone(net):
    print("\nThere at least one person that knows everyone.")
else:
    print("\nThere is nobody that knows everyone.")

print("\nWe are now ready to recommend a friend for a user you specify.")
uid=get_uid(net)
rec=recommend(uid, net)
if rec==None:
    print("We have nobody to recommend for user with ID", uid, "since he/she is dominating in their connected component")
else:
    print("For user with ID", uid,"we recommend the user with ID",rec)
    print("That is because users", uid, "and",rec, "have", len(getCommonFriends(uid,rec,net)), "common friends and")
    print("user", uid, "does not have more common friends with anyone else.")
        

print("\nFinally, you showed interest in knowing common friends of some pairs of users.")
print("About 1st user ...")
uid1=get_uid(net)
print("About 2st user ...")
uid2=get_uid(net)
print("Here is the list of common friends of", uid1, "and", uid2)
common=getCommonFriends(uid1,uid2,net)
for item in common:
    print(item, end=" ")



