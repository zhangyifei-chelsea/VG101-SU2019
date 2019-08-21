# vg101: Introduction to Computer Programming 

## Mid1 RC Plotting and Data Structure


### Outline

* Lectures
  * Plotting
  * Advanced topics
    * Data types
    * Structures

### Lectures


#### Plotting
Matlab has a whole catalog including all the plotting related information in **Graphics** (under Documentation -> MATLAB -> Graphics).  

##### Common used functions
- axes: create, and specify the range of axes in the current figure window
- plot: create a new plot, will cover the prev plot in the same figure window
- hold on/off: retain (or not) the current plot when adding new plots 
- subplot: ```subplot(m, n, p)```
- title: add title on the top of a figure (LaTeX syntex supported)
- xlabel/ylabel: set axis labels (LaTeX syntex supported)
- line: ``` line([x0 x1],[y0 ,y1])``` Draw a line from (x0, y0) to (x1, y1)
- rectangle: ```rectangle('Position',[left_down_x0 left_down_y0 width height])```  
   Lines and rectangles are annotations, so no need to use *hold on* 
- clf: delete all the graphics objects on the current figure, replot evereything afterwards 

#### Advanced topics

##### Data type 
- What is data type? Why we need it?
    - Each variable has a specific data type
    - It tells the interpreter how to allocate memory and how to load and interpret some bits at certain address in memory
    - It defines the operations a certain variable can have
- Different data types in Matlab  
    - int: int8, int16, int32, int64  
      The most significant bit is the sign bit.  
    - uint: uint8, uint16, uint32, uint64
    - single(32 bit), double(64 bit)
    - logical
    - char (single quotation mark), string(double quotation mark)  
        - provide storage for text data, but string array treats each phrase as a unit, whereas a char array treats each character as a unit   
        - their ways for storage data is likely to be different  
    eg: Try this in command window
    ```matlab
    chr='abcd';
    chr(1)
    whos chr
    str="abcd";
    str(1)
    whos str
    ```  
        - string specfic functions are both suitable for *string* and *char array* (like str2num, strcmp, strfind, strrep), but the data type of the return value may be affected by your choice
    - cell array
    - structure
    - function handle
    - classes
- Type Conversion  
There are many ways to convert one data type into another in MATLAB.  
eg. convert string into double
```matlab
str = "123.45";
db = str2double(str); % similar to int2str, mat2str, num2str, str2num

db = cast(str,'double')

db = double(str);
```
