# **Lab Report 4 - Week 8**
### _By: Zhicheng Wang, Pid: A16869487_

![ChMkJlbKw0WIcjXGAA--xnhwdi4AALG0QOAIDAAD77e961](https://user-images.githubusercontent.com/97211608/155808012-ab2fc7c3-5efb-4e53-80fe-2c25455232c5.jpg)

## Links
**[Link to our markdown-parse repository](https://github.com/ezhou413/markdown-parse)

**[Link to the one we reviewed](https://github.com/sm52/markdown-parse)

## Snippet 1 
```
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```
## VScode preview of Snippet 1

<img width="326" alt="截屏2022-02-25 下午1 52 26" src="https://user-images.githubusercontent.com/97211608/155808129-19048715-b67f-4cd9-b3c4-d1a1b8355825.png">

- According to VScode, the last three lines count as links while the first doesn't

## Turning Snippet 1 into test 
```
 @Test
 public void testSnippet1() throws IOException {
      Path fileName = Path.of("snippet1.md");
	    String contents = Files.readString(fileName);
      ArrayList<String> links = MarkdownParse.getLinks(contents);

      assertEquals(List.of("`google.com","google.com","ucsd.edu"),links);

    }
```
### Screenshot in `MarkdownParseTest.java`

<img width="515" alt="截屏2022-02-25 下午3 20 00" src="https://user-images.githubusercontent.com/97211608/155815863-e9acedc5-25cb-490e-9b3f-ba0caffe3fd7.png">


### My implementation 

<img width="545" alt="截屏2022-02-25 下午3 19 31" src="https://user-images.githubusercontent.com/97211608/155815898-32fd4a0e-1034-4529-bee9-ee05c838fae5.png">

_Sadly it failed_ 

### implementation we reviewed 

<img width="678" alt="截屏2022-02-25 下午3 22 43" src="https://user-images.githubusercontent.com/97211608/155816126-1f9cd168-2bb6-42f4-a31e-9886664b7bc5.png">

_It failed as well :(_

## Snippet 2
```
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```
## VScode preview of Snippet 2

<img width="263" alt="截屏2022-02-25 下午2 43 43" src="https://user-images.githubusercontent.com/97211608/155813009-573eaa6a-86b3-4107-9051-e89a4abfd7ec.png">

- According to VScode, only the `b.com` doesn't count as a link

## Turning Snippet 2 into test 
```
 @Test
 public void testSnippet2() throws IOException {
      Path fileName = Path.of("snippet2.md");
      		String contents = Files.readString(fileName);
      ArrayList<String> links = MarkdownParse.getLinks(contents);

      assertEquals(List.of("a.com","a.com(())","example.com"),links);

    }
```
### Screenshot in `MarkdownParseTest.java`

<img width="539" alt="截屏2022-02-25 下午2 46 23" src="https://user-images.githubusercontent.com/97211608/155813222-91972795-9932-4bd9-a47d-4358c8bb663a.png">

### My implementation 

<img width="672" alt="截屏2022-02-25 下午2 49 33" src="https://user-images.githubusercontent.com/97211608/155813459-629a5cc8-c223-4bae-903c-bb94bc7a7fbe.png">

_failed again_

### implementation we reviewed 

<img width="676" alt="截屏2022-02-25 下午2 48 11" src="https://user-images.githubusercontent.com/97211608/155813360-c2b8cb33-90b7-44e7-b808-356632a0ad1f.png">

_failed again_

## Snippet 3
```
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
    https://ucsd-cse15l-w22.github.io/
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text
```
## VScode preview of Snippet 3

<img width="296" alt="截屏2022-02-25 下午2 54 51" src="https://user-images.githubusercontent.com/97211608/155813894-26f2e7b2-1a92-46aa-894d-84dea5831542.png">

## Turning Snippet 3 into test 
```
 @Test
 public void testSnippet3() throws IOException {
      Path fileName = Path.of("snippet3.md");
      		String contents = Files.readString(fileName);
      ArrayList<String> links = MarkdownParse.getLinks(contents);

      assertEquals(List.of("https://www.twitter.com",
      "https://ucsd-cse15l-w22.github.io/",
      "https://cse.ucsd.edu/"),links);

    }
```
### Screenshot in `MarkdownParseTest.java`

<img width="487" alt="截屏2022-02-25 下午2 56 09" src="https://user-images.githubusercontent.com/97211608/155814013-3de43f6b-258f-45df-839c-2e593682df76.png">

### My implementation 

<img width="568" alt="截屏2022-02-25 下午3 30 27" src="https://user-images.githubusercontent.com/97211608/155816729-2efda264-01ac-4a90-8fa7-6867b9dce6f2.png">


_failed again_

### implementation we reviewed 

<img width="589" alt="截屏2022-02-25 下午3 02 18" src="https://user-images.githubusercontent.com/97211608/155814536-eb4b605b-6119-45bf-8ee7-8500dcf3da77.png">

_failed again_

## Small code change regarding snippet 1? 

- I do think that a small code change could solve this problem. I am currently thinking of that if the substring of the `nextOpenBracket` and `nextCloseBracket` contains a backtick and that there is a backtick "just" before the link statement, then we would use `continue` and `currentIndex = closeParen + 1` to go on the next iteration and look for the next `nextOpenBracket`.

## Small code change regarding snippet 2? 

- For this one, I also think that it is possible to fix with a small code change. My idea is that we use a while loop and that if the current `nextCloseBracket` has a close bracket after it then we would set `nextCloseBracket=nextCloseBracket+1`. The loop will stop if it reaches the end of the file (markdown.length) or if `charAt(nextCloseBracket+1)!="]"`. And the same idea goes with the `closeParen`.

## Small code change regarding snippet 3? 

- This test was just ridiculous and it would definitly be a more involved change since the expected output and the actual output were worlds apart. I don't even know how to approach this problem because the VScode preview only sees the `https://cse.ucsd.edu/` as a link while our code takes on the whole

```
github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/
```

- Which to a certain extend, I would actually think that our code was more "correct" on this part

# The END
(sorry for writing a bit pass the 2-3 sentences limit)
