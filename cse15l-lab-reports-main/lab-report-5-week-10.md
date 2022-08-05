# **Lab Report 5 - Week 10**
### _By: Zhicheng Wang, Pid: A16869487_

## Finding tests with different results
- I used `diff` on the results of running a bash for loop

- I first clone the [https://github.com/ucsd-cse15l-w22/markdown-parse](https://github.com/ucsd-cse15l-w22/markdown-parse) repository into `ieng6`

- Then run `bash script.sh > results.txt` which is a for loop on all the test-files that is in `.md` and then it will store all the results in `results.txt`

_script.sh_

```
for file in test-files/*.md;
do
  echo $file 
  java MarkdownParse $file
done
```

- Then I copy over the `test-files` and `script.sh` to my implementation of markdown-parse and do the above as well

```
//copy over test-files
cp -r markdown-parse/test-files my-markdown-parse/

//copy over script.sh
cp markdown-parse/script.sh my-markdown-parse/
```

### Now we have 2 `results.txt`files and we can use the `diff` command 

```
$ diff my-markdown-parse/results.txt markdown-parse/results.txt 
```

<img width="740" alt="截屏2022-03-10 下午4 12 00" src="https://user-images.githubusercontent.com/97211608/157776796-3a25a909-7fc2-43a0-8ad8-3349b622be60.png">

## Test 1

```
230c230
< []      //our output
---
> [baz]   //lab 9 implementation output
```

- The 230 means line 230 in `results.txt` and thanks to `echo` we know what file that will refer to

(the following is from Remote Explorer in VSCode)

<img width="633" alt="截屏2022-03-10 下午4 27 08" src="https://user-images.githubusercontent.com/97211608/157778194-056b55d8-278e-4e37-b5c6-ea283896002e.png">

- We can see that is from `test-files/201.md` so we just cat into it and check out the file

```
$ cat markdown-parse/test-files/201.md
```

<img width="509" alt="截屏2022-03-10 下午4 27 37" src="https://user-images.githubusercontent.com/97211608/157778240-649f2886-3db7-45a6-b458-2f7f94572e97.png">

### According to VSCode, there are no links in the file

- I just copy the output from `cat` and paste into a new md file and preview it

<img width="819" alt="截屏2022-03-10 下午4 28 20" src="https://user-images.githubusercontent.com/97211608/157778304-06748dd8-89a4-42e5-88fb-6fe83a6128f5.png">

- It is clear that our implementation of markdown-parse was correct on this test and the expected output should be empty

## What is wrong with lab 9 implementaion?

- The problem here is that for the lab 9 markdown-parse implementation, it didn't account for a case where the closed bracket `]` is not next to the open paranthesis `(`
which can be fixed easily by adding the following if statement after the while loop

<img width="450" alt="截屏2022-03-10 下午4 40 41" src="https://user-images.githubusercontent.com/97211608/157779485-2328f258-b3d5-4578-bad5-71c10a7e7a36.png">

so that the implementation won't see this as a link 

_Note: this fix is specifically for this case_

## Test 2

```
928c928
< []          //our output
---
> [moon.jpg]  //lab 9 implementation output
```

- line 928 would be corresponding to `test-files/516.md`

<img width="543" alt="截屏2022-03-10 下午5 00 33" src="https://user-images.githubusercontent.com/97211608/157781452-eace315b-5948-4dfe-89be-a533a4470508.png">

- `cat` into the file 

<img width="546" alt="截屏2022-03-10 下午5 01 37" src="https://user-images.githubusercontent.com/97211608/157781553-de2d746d-4e7c-4627-a408-aef0f0e08135.png">

### According to VSCode, there are no links in the file but is does count as an image

<img width="806" alt="截屏2022-03-10 下午5 02 03" src="https://user-images.githubusercontent.com/97211608/157781599-0dcd0054-65fe-4c5f-a819-b0c5616acc60.png">

- So our implementation was correct on this test case as well

## What is wrong with lab 9 implementaion?

- It doesn't check the case where image in markdown has similar structures and should not be count as links 

we can add the following if statement after the while loop 
```
if (!(markdown.charAt(nextOpenBracket-1) == '!')) {
                        toReturn.add(markdown.substring(openParen + 1, closeParen));
                    } 
```
which would only add links where if there is an exclamation mark in front of open bracked, 
it won't be counted as a link

# The End~~~~ 
### yayyyy we're done with this course~~ thank you for all your hard works!

