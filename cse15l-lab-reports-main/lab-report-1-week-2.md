## Welcome to Zhicheng's first lab report!!!!

![https---specials-images forbesimg com-imageserve-617853670-Drive-by-hacker-960x0 jpg?fit=scale](https://user-images.githubusercontent.com/97211608/149288135-be00f80e-86a7-4427-b4b0-72a4bad9f2f5.jpeg)


### Let's begin the Tutorial !!!

# Visual Studio Code

1. First, You need to download [Visual Studio Code](https://code.visualstudio.com) on your computer. After it is installed, double click the icon and you will end up in a screen which looks something like this. 

<img width="1024" alt="截屏2022-01-12 下午11 14 40" src="https://user-images.githubusercontent.com/97211608/149283051-fae79476-3c5c-4aff-bbd6-0204ace0fb86.png">

# Remotely Connecting

- Window users need to [install OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

Next, each student have their own course-specific account which can be found at: [Account Lookup](https://sdacs.ucsd.edu/~icc/index.php)


_Note: for CSE15L, our account starts with **cs15lwi22**_


Enter the following command but replace `abc` with the letters of your course-specific account 


```
ssh cs15lwi22abc@ieng6.ucsd.edu
```

If this is your first time connecting to a server, you will get a message like this:
```
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
```
We usually type `yes` in this case and then it will ask for your password!

After you successfully logged in with your password, the output should look like this：

<img width="686" alt="截屏2022-01-13 下午5 49 07" src="https://user-images.githubusercontent.com/97211608/149437544-1fce6089-df67-437d-8768-1875fbbbded7.png">

If you made it this far, congrats! Your terminal is now connected!!!

# Trying Some Commands

Below are some commands you can try on your own:

- `cd~`  navigate to your home directory
- `cd` navigate to your home directory
- `ls -lat` list latest files sorted with dates
- `ls -a` list all files
- `ls<directory>` where `<directory>` is `/home/linux/ieng6/cs15lwi22/cs15lwi22abc/`
- `cp /home/linux/ieng6/cs15lwi22/public/hello.txt ~/`
- `cat /home/linux/ieng6/cs15lwi22/public/hello.txt`

**Sample Outputs:**

<img width="783" alt="截屏2022-01-13 下午9 57 06" src="https://user-images.githubusercontent.com/97211608/149458985-d7948bdb-ce3b-4432-8b58-e9628ab28846.png">

**Logout command:**

- `exit`

After typing in `exit` you should receive the following message:

<img width="471" alt="截屏2022-01-13 下午7 39 48" src="https://user-images.githubusercontent.com/97211608/149447606-315fce80-e936-490d-af7d-83fb30561b38.png">

# Moving Files with scp

- To start, we need to create a file called `WhereAmI.java` and copy and paste the following:

```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```

**To run the file on server, you need to run the command:**

`scp WhereAmI.java cs15lwi22abc@ieng6.ucsd.edu:~/` 

- replace `abc` with your letters
- then log in with `ssh` and use `javac` and `java` 

You should get the follwing:

<img width="553" alt="截屏2022-01-13 下午10 15 06" src="https://user-images.githubusercontent.com/97211608/149460641-e145389c-8771-45e7-8bc6-7efac4dfa182.png">

## Running on client output:

<img width="598" alt="截屏2022-01-13 下午10 13 15" src="https://user-images.githubusercontent.com/97211608/149460493-2c06bbc1-ebfa-4c80-974a-00cfc9efb06a.png">

# Setting an SSH Key

- used so we don't have to type our password every single time

the command of creating such key is called `ssh-keygen`

**The following is how you set it up:**

<img width="665" alt="截屏2022-01-13 下午10 32 59" src="https://user-images.githubusercontent.com/97211608/149462307-f35d9d22-3ccc-4879-8485-24e9d053678c.png">

**Then copy the public key to the `.ssh` directory**

<img width="663" alt="截屏2022-01-13 下午10 44 58" src="https://user-images.githubusercontent.com/97211608/149463470-343f042e-8b4a-4b87-9ef6-03e5a3d53161.png">

**Now we don't need to enter passwords anymore!!! HOORAY**

<img width="657" alt="截屏2022-01-13 下午10 45 33" src="https://user-images.githubusercontent.com/97211608/149463534-90929767-8704-4962-93a5-2f68d0842270.png">

# Optimizing Remote Running

- You can write quotes at the end of an `ssh` command to run it directly on the server

<img width="655" alt="截屏2022-01-13 下午10 56 35" src="https://user-images.githubusercontent.com/97211608/149464655-ec9325e0-4dd8-4b38-85a7-dcefc9d8e545.png">

- You can also use semicolons to run multiples commands

<img width="663" alt="截屏2022-01-13 下午10 57 42" src="https://user-images.githubusercontent.com/97211608/149464778-a67b2a57-462d-4788-b8c6-8b9ce2dd3c60.png">

- You can also use the up-arrow on your keyboard to accese previous inputs

### THE END
