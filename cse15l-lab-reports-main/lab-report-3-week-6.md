# **Lab Report 3 - Week 6**
### _By: Zhicheng Wang, Pid: A16869487_

![1644386274583542](https://user-images.githubusercontent.com/97211608/153555814-bc088786-6921-431d-9690-c4838356807a.jpg)

# _Task_: **Copy whole directories with `scp -r`**

## Copying markdown-parse Directory to ieng6 account

- Run the following command

```
scp -r . cs15lwi22@ieng6.ucsd.edu:~/markdown-parse
```

<img width="613" alt="截屏2022-02-11 上午1 55 11" src="https://user-images.githubusercontent.com/97211608/153571105-af7033b0-7e99-46ac-a231-6ae6471f8154.png">

- The above is just part of the process when copying the whole directory ! 

- Notice that there were a lot of "extra" stuff that is also being copied to the remote server.

## Compiling and Running the tests in ieng6 account 

<img width="573" alt="截屏2022-02-11 上午1 58 58" src="https://user-images.githubusercontent.com/97211608/153571668-b83d7e3c-7684-4700-be2d-021ab906a90a.png">

- After logging into the ieng6 account and using the `ls markdown-parse` command, we can see that all the files have been copied over, even the ones we would see in `.git`

_Then after `cd` into `markdown-parse`_

- We can now compile and run the tests for our repository !

<img width="617" alt="截屏2022-02-11 上午1 59 47" src="https://user-images.githubusercontent.com/97211608/153571792-e5e49caf-040c-445b-84b4-50da783b9818.png">

- All 8 tests passed with no errors :)

## Combining `scp`, `;`, and `ssh` to copy the whole directory and run the tests in one line

 ``` 
$ scp -r . cs15lwi22awg@ieng6.ucsd.edu:~/markdown-parse; 
ssh cs15lwi22awg@ieng6.ucsd.edu 
"cd markdown-parse; javac -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar MarkdownParseTest.java;
java -cp .:lib/junit-4.13.2.jar:lib/hamcrest-core-1.3.jar org.junit.runner.JUnitCore MarkdownParseTest"

 ```
 - We can see that in this one line of code, the files have been successfully copied and we connected to the server with all the tests compile and running 
 
<img width="601" alt="截屏2022-02-11 上午2 09 00" src="https://user-images.githubusercontent.com/97211608/153573168-45196e97-0e1a-44c6-8d6d-052a7220aacb.png">

## The END
