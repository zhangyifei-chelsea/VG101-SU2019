# lab7
## Homework 6
### ex4
- read the file (do not forget `fclose` at the end)  
```c
FILE *input;
input=fopen("matrices.txt","r");
%
```
 pay attention that the path should be relative path instead of absolute path, since absolute path depends on your own computer
- Judge the size of the matrix  
   The size can be judged in two ways
   - (number of lines-1)/2
   - number of spaces in the first line + 1  
   rewind the file if necessary (set the pointer back to the beginning of the file)  
```c
int n=0;
char c='1';
    while(c!='\n')
    {
        c=fgetc(input);
        if(c==' ')
            ++n;
    }
    rewind(input);
%
```
- malloc 2D array
```c
int** A=malloc(n*sizeof(int *));
for(int i=0;i<n;++i)
{
    A[i]=malloc(n* sizeof(int));
}
\\
```
- read the file and store numbers into the matrix
```c
for(int i=0;i<n;++i)
{
    for(int j=0;j<n;++j)
    {
        fscanf(input,"%d",&A[i][j]);
    }
}
\\
```
- do matrix arithmetics
- free 2D array
```c
for(int i=0;i<n;++i)
    free(A[i]);
free(A);
//
```


### ex5
- understand the problem: 
```c
typedef struct universalSet { void *elem; int card; int type; } uset;
```
   -  `elem` is the pointer to the elements of the set
   -  `card` is the cardinality
   -  `type` is the data type of the elements stored in the set
- `**` v.s. `*`  
  If we only need to modify the contents, pass `*`. If we also may modify the address of the contents, pass `**` and so on.  
  Here it can be `void newSet(uset *set, int type);` and  `void deletSet(uset *set);`, since the address of set will not change in the function.  
  One hint: realloc may change the address the pointer is pointing to
- type casting v.s. direct memory operation
   - type casting
```c
// if we are dealing with the char case
char *set_ele = set->elem;
char add_ele = (*(char *) elem);
// then add of remove elements
//
```
   - memory operation (memcmp&memcpy)
```c
memcmp(elem, (void *) ((size_t) set->elem + i * set->type), (size_t) set->type) // compare the new element `elem` with the i th element of the set
memcpy((void *) ((size_t) set->elem + set->card * set->type), elem, (size_t) set->type); //copy the value of the new `elem` to the end of the set
\\
```

### ex6
- Insert First List  
```c
\\ how to call it
node_t *list1 = Initialize(...);
InsertFirstList(&list1, ch);
\\ function body
void InsertFirstList(node_t **head, char insert_char)
\\malloc a new node
\\let new_node->next point to the original head
\\let head point to the address of the new node
\\since the address head pointing to may change, we need node_t **head
\\
```
- Insert Last
  1. malloc a new_node
  2. check if the list is empty. If it is directly insert this new_node, if it is not, move to the end of the list, insert it there.
- Delete First
  1. if the list is empty, return
  2. move the head to head->next, free the original head
- Delete Last
  1. if the list is empty, return
  2. if the list has only 1 element, free the element, let `*head=NULL`
  3. if the list has more than 1 elements, set two pointer `ptr1, ptr2` one follow another, move `ptr2` to the end, free it, and set `ptr2->next=NULL`
- Merge
  1. append list2 after list1
  2. set list2 to NULL (not necessary, but need to do this to pass JOJ)
- Split
  1. `if pos == 0, set *tail=*head, set *head=NULL`
  2.  move a pointer `tmp` to the (pos-1) th node of the list. If the list is not long enough, directly return
  3. let `*tail=tmp->next` and let `tmp->next=NULL`

## recursion revisit
### Generate binary numbers
`
Generate decimal number only composed of 0 or 1
`
### Generate valid parentheses 
`
Given n pairs of parentheses, write a function to generate all combinations of well-formatted parentheses.
`  
Use backtracing:  
Only provide pseudocode
```
Function generate(left, right, solution_set, current_string)
    if (left == 0 and right == 0)
        add current_string to solution_set
    if (left > 0)
        generate(left-1, right, solution_set, current_string + '(')
    if (right > left)
        generate(left, right-1, solution_set, current_string + ')')
%        
```

## Lab 5
```c
struct node  
{ 
    country_t* country; 
    struct node *left; 
    struct node *right; 
}node_t;
//
```
### Initialize a binary tree
malloc the root node in your main, then call this init function on root.
```c
void init(node_t *root, int level)
{
    if (level == 0)
    {
        root->left = NULL;
        root->right = NULL;
        return;
    } else
    {
        root->left=malloc(sizeof(node_t));
        root->right=malloc(sizeof(node_t));
        init(root->left,level-1);
        init(root->right,level-1);
    }
}
//
```
### Post-order transversal to get winners
```
function Postorder(node_t* root)  
    if (root == NULL) 
        return; 
    Postorder(root->left, k);
    Postorder(root->right, k);
    root->country = get_winner(root->left->country, root->right->country , k);
//
```
### Free it
```c
void free_tree(node_t* root)
{
    if(root!=NULL)
    {
        free_tree(root->left);
        root->left=NULL;
        free_tree(root->right);
        root->right=NULL;
        free(root);
    }
}
//
```
use valgrind to check memory leak!
