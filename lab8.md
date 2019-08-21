# lab8
## ex3
take advantage of fstream sstream and some STL containers.   
- fstream example
```cpp
ifstream input_file("matrices.txt");
//...
input_file.seekg(0); // like rewind
input_file.close();
//
```
- sstream example: 
```cpp
string line;
getline(input_file, line);
istringstream iss(line);
int num;
size_t n = 0;
while (iss >> num) n++;
//
```
- store matrix:
    - strategy 1: 2D array (c++ forbiden VLA)
```cpp
int** A=new int*[k];
for(int i=0;i<k;++i)
{
    A[i]=new int[k];
}
for (int i = 0; i < n; i++)
{
    for (int j = 0; j < n; j++)
    {
        input_file >> A[i][j];
    }
}
// do not forget to delete them
//
```
    - strategy 2: vector
```cpp
vector<vector<int>> data(n, vector<int>(n));  // refer to http://www.cplusplus.com/reference/vector/vector/vector/
// then fill in numbers with loop
//
```

## ex4
(optinal) use dynamic programming: store all intermediate values  
creating a table to record all N value for 2-M recursively, summerize return the index of the maximum value   
Algorithm:  
```
// in main, create a vector of size M+1 to store N values, pass the ref of it into the recursive function
function find_N(vector<int> &data, unsigned long long num)
    if num is a valid index of `data`, and data[num]>0, return data[num];
    if num==1, return 0;
    Init N as 0;
    if num%2==0  N=find_N(data,num/2)+1;
    else  N=find_N(data,num*3+1)+1;
    if num is a valid index of `data`, data[num]=N;
    return N;
end function
```
