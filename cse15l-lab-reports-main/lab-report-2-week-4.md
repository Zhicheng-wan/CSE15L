# **Lab Report 2 - Week 4**
### _By: Zhicheng Wang, Pid: A16869487_

![58b180bcba5a92d7d95c58153c9ce5b2](https://user-images.githubusercontent.com/97211608/151492971-df483ed3-2d93-4421-a578-2a8e64d8eb46.png)

# **First Code Change**

## Code Change Difference From Github
<img align="right" width="1255" alt="截屏2022-01-27 下午10 00 44" src="https://user-images.githubusercontent.com/97211608/151495399-4df07f75-1061-4aad-bfa9-961a9060ecae.png">

## Link To The Test File
- [Click Me!!!](https://github.com/Jackson-Wang-0/cse15l-lab-reports/blob/main/test-file-new.md)

## Symptom of Failure-inducing Input
<img width="646" alt="截屏2022-01-27 下午10 18 17" src="https://user-images.githubusercontent.com/97211608/151497395-2eff180e-6d6a-42ab-ba40-9149c796292d.png">

- The symptom was that it was producing wrong outputs. Instead of **"only"** printing out the links of the file, it also printed out the image link. 

- This happens due to a bug in our code where whenever we see the following sequence in a file. We tend to store whatever is between the paranthesis into our array.
```
[]()
```

- **We can fix this bug by realizing that image always comes with an exclamation mark `!`** 

**_Therefore, we add the following if condition_**

```
if (!(markdown.charAt(nextOpenBracket-1) == '!')) {
                 toReturn.add(markdown.substring(openParen + 1, closeParen));
             }
```
Where we would only store a link if it's open bracket doesn't come with an exclamation mark `!` before it, and that would fix the bug!


# **Second Code Change**

## Code Change Difference From Github
<img width="1225" alt="截屏2022-01-27 下午10 46 13" src="https://user-images.githubusercontent.com/97211608/151500514-f1662a6c-bae7-472a-9b8b-aea9d8822249.png">

## Link To The Test File
- [Click Me Again!!!](https://github.com/Jackson-Wang-0/cse15l-lab-reports/blob/main/test-file7.md)

## Symptom of Failure-inducing Input
<img width="630" alt="截屏2022-01-27 下午10 58 43" src="https://user-images.githubusercontent.com/97211608/151501858-4612397c-cf66-4a8d-a65a-56420b332cb0.png">

- The symptom was that our program throws an out of memory exception instead of printing out an array with no elements in it

- The bug was caused by the test file having the closing paranthesis `)` at index 0 and doesn't have the opening parenthesis `(` and the closing bracket `]` which will not update our `currentIndex` variable and result in an infinite loop that would eat up all the memory 

- **We know that ')' cannot be at index 0 and we need all of the characters of the sequence** 

_To remind you of what sequence I'm referring to_

```
[]()
```

**_Therefore, we add the following if condition_**

```
if (nextOpenBracket == -1 || nextCloseBracket == -1 || openParen == -1 || closeParen == -1) {
                currentIndex++;
                continue;
            }
```
Where if one of the characters is not found (aka. has index of -1). We will increase the `currentIndex` variable by 1 and go to the next iteration.

# **Last Code Change**

## Code Change Difference From Github
<img width="1095" alt="截屏2022-01-28 上午12 30 12" src="https://user-images.githubusercontent.com/97211608/151513249-0442dbd3-42d6-44c3-bc25-1b54b710cd6b.png">


## Link To The Test File
- [Click Me For the Last time :)](https://github.com/Jackson-Wang-0/cse15l-lab-reports/blob/main/test-file8.md)

## Symptom of Failure-inducing Input
<img width="708" alt="截屏2022-01-27 下午11 35 57" src="https://user-images.githubusercontent.com/97211608/151506076-a283eb98-99f4-4337-a122-4c3b72281d69.png">

- The symptom was that it threw a StringOutOfIndexException instead of printing out nothing since there is an opening bracket `[` that was after the closing paranthesis `)` 

- The bug was that our program wouldn't realize this situation and stores the next open bracket during the second iteration we see in the file which has an index of 0 after we updated `currentIndex`. Then when we want to check if the index before `nextOpenBracket` by using `charAt(nextOpenBracket-1)` to tell whether or not that it was a image link, it would throw the StringOutOfIndexException.

- **We know that ')' cannot be at index 0 and we need all of the characters of the sequence** 

**_Therefore, we add the following if statement_**

```
 if(nextOpenBracket!=0){
                if (!(markdown.charAt(nextOpenBracket-1) == '!')) {
                    toReturn.add(markdown.substring(openParen + 1, closeParen));
                } 
            }
```
Which insures that if `nextOpenBracked` is not at index 0 , then we will check if it is a image link.

**Note: This end up making test-file5.md not passing the test so we could adjust it to the following**
```
if((nextOpenBracket!=0) && (openParen-nextCloseBracket==1)){
                if (!(markdown.charAt(nextOpenBracket-1) == '!')) {
                    toReturn.add(markdown.substring(openParen + 1, closeParen));
                } 
            }
```
Now all cases PASS!!!!

# **The End**
# Thanks for taking your time reading this!!!


