### Binura Gunasekera
### Assignment 5: Classes / Recursion
### ITI 1120 [D]
### 300021973

class Point:
    'class that represents a point in the plane'

    def __init__(self, xcoord=0, ycoord=0):
        ''' (Point,number, number) -> None
        initialize point coordinates to (xcoord, ycoord)'''
        self.x = xcoord
        self.y = ycoord

    def setx(self, xcoord):
        ''' (Point,number)->None
        Sets x coordinate of point to xcoord'''
        self.x = xcoord

    def sety(self, ycoord):
        ''' (Point,number)->None
        Sets y coordinate of point to ycoord'''
        self.y = ycoord

    def get(self):
        '''(Point)->tuple
        Returns a tuple with x and y coordinates of the point'''
        return (self.x, self.y)

    def move(self, dx, dy):
        '''(Point,number,number)->None
        changes the x and y coordinates by dx and dy'''
        self.x += dx
        self.y += dy
        

    def __eq__(self, other):
        '''(Point,Point)->bool
        Returns True if self and other have the same coordinates'''
        return self.x == other.x and self.y == other.y
    def __repr__(self):
        '''(Point)->str
        Returns canonical string representation Point(x, y)'''
        return 'Point('+str(self.x)+','+str(self.y)+')'
    def __str__(self):
        '''(Point)->str
        Returns nice string representation Point(x, y).
        In this case we chose the same representation as in __repr__'''
        return 'Point('+str(self.x)+','+str(self.y)+')'

class Rectangle:
    'class that represents rectangle in the plane'

    
    def __init__(self,botLeft,topRight,color):
        
        self.x = botLeft
        self.y = topRight
        self.color = color



    def __repr__(self):
        """ Overwrites pythons REPR builtin. """    
    
        return 'Rectangle('+str(self.x)+', '+str(self.y)+", '"+str(self.get_color())+"')"

    
        
    def get_bottom_left(self):
        """ Method that returns bottom left coordinate Point of Rectangle Object. """  
        return (self.x)



    def get_color(self):
        """ Method that returns color of rectangle. """    
        return (self.color)



    def get_top_right(self):
        """ Method that gets top right coordinate Point of rectangle Object. """  
        return (self.y)


    
    def reset_color(self,newcolor):
        """ Changes color attribute of Rectangle Object. """
        self.color = newcolor



    def get_perimeter(self):
        """ Calculates perimeter of any given Rectangle Object using it's x,y coordinates. """   
        height = self.y.y - self.x.y
        base = self.y.x - self.x.x
        return 2*height + 2*base


    
    def get_area(self):
        """ Calculates area of any given Rectangle Object using it's x,y coordinates. """    
        return (self.y.y-self.x.y)*(self.y.x-self.x.x)


    
    def move(self,dx,dy):
        
        self.x.move(dx,dy)
        self.y.move(dx,dy)


        
    def __eq__(self,other):
        """ Overwrites Python's EQ Builtin. """   
        return self.x == other.x and self.y == other.y and self.color == other.color


    
    def intersects(self,other):
        """ Checks if any two rectangle objects intersect on any given 2-D plane. """   
        if other.y.y < self.x.y or other.x.y > self.y.y:
            return False
        elif other.x.x > self.y.x or other.y.x < self.x.x:
            return False
        return True


    
    def contains(self,x,y):
        """ Checks if any given Rectangle Object has a point of coordinates (x,y) in its' space. """    
        if y < self.x.y or y > self.y.y:
            return False
        elif x > self.y.x or x < self.x.x:
            return False
        return True


    
    def __str__(self):
        """ Overwrites Python's STR Builtin. """   
        return("I am a"+', '+str(self.color)+' rectangle with bottom left corner at ' + str(self.x) +' and top right corner at '+str(self.y)+'.')

        
class Canvas:
    """ class that represents a conglomerate of rectangles in a plane. """



    def __init__(self,L=[]):
        
        self.contents = L


        
    def add_one_rectangle(self,name):
        """ Adds a rectangle into the Canvas rectangle list. """   
        self.contents.append(name)


        
    def __repr__(self):
        """ Overwrites Python's REPR Builtin. """   
        return 'Canvas('+str(self.contents)+')'

    
        
    def __len__(self):
        """ Overwrites Python's LEN Builtin. """
        return len(self.contents)



    def count_same_color(self,color):
        """ Counts the amount of Rectangles of the same color attribute in any given Canvas """   
        color_count = 0
        for i in range(len(self.contents)):
            if self.contents[i].get_color() == color:
                color_count += 1
        return color_count



    def total_perimeter(self):
        """ Calculates the perimeter of all rectangles inside the Canvas """   
        complete_perimeter = 0
        for i in range(len(self.contents)):
            complete_perimeter += self.contents[i].get_perimeter()
        return complete_perimeter



    def min_enclosing_rectangle(self):
        """ Finds the rectangle of minimum dimensions that can contain all rectangles in the Canvas """    
        bottomLeft = []
        topRight = []
        minLeft = []
        minHeight = []
        maxRight = []
        maxHeight = []
        for i in range(len(self.contents)):
            bottomLeft.append(self.contents[i].get_bottom_left())
            topRight.append(self.contents[i].get_top_right())
        
        for i in range(len(bottomLeft)):
              minLeft.append(bottomLeft[i].x)
              minHeight.append(bottomLeft[i].y)
        
        for i in range(len(topRight)):
            maxRight.append(topRight[i].x)
            maxHeight.append(topRight[i].y)
        minLeft.sort()
        minHeight.sort()
        maxRight.sort(reverse=True)
        maxHeight.sort(reverse=True)
        
        print("Rectangle(Point("+str(minLeft[0])+","+str(minHeight[0])+"),Point("+str(maxRight[0])+","+str(maxHeight[0])+"),'red')")



    def common_point(self):
        """ Checks if all the rectangles have one common intersection (Returns True if there is one, else False) """
        RList = []
        for i in range(len(self.contents)):

            for j in range(len(self.contents)):
                if self.contents[i].intersects(self.contents[j]) == False:
                    return False
        return True
                



