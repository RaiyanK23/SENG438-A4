**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#4 – Mutation Testing and Web app testing**

| Group \#:  20    |     |
| -------------- | --- |
| Jacob Adeyemo | 30046186 |
| Mohammed Kabir | 30092222 |
| Kundai Dziwa | 30090173 |
| Markosch Saure | 30088690 |

# Introduction
Lab 4 for SENG 438 requires us to apply the concepts of both mutation and GUI testing that we have learned during lectures. We know that mutation testing is injecting bugs (mutants) into our SUT and then testing those mutants against our existing test suite (assignment 2 and 3) to see how effective it is in terms of the mutation score and if we can effectively "kill" the mutants, and will use tools such as PIT to aid us with this.

GUI testing will similarly use tools, specifically Selenium web-interface testing tool as well as Sikulix to create automated GUI testing as well as manual testing. This will involve testing at least one of the websites: Costco page, Ikea page or Amazon page. Ultimately, we will create UI test cases (8) and then automate them using Selenium and then report how it fares against Sikulix.

# Analysis of 10 Mutants of the Range class 
1. Incremented (a++) double local variable 

This mutation is created when pitest modifies the source code by imcrementing the specified local variable which is of type double by 1 after it is passed, basically post increments the variable. To give an instance if the double x = 1 it would be mutated to double x = 2.

In our original test suite this mutation was killed in some test cases and in others it survived. We believe that the mutation survived in some cases beacuse the change lasted throughout the method and the mutation was killed if the change was overwritten by future code in the method before the return statement.

2. Decremented (--a) double local variable 

This mutation is created when pitest modifies the source code by decrementing the specified local variable which is of type double by 1 after it is passed, basically pre decrements the variable. To give an instance if the double x = 2 it would be mutated to double x = 1.

In our original test suite this mutation was killed in some test cases and in others it survived. We believe that the mutation survived in some cases beacuse the change lasted throughout the method and the mutation was killed if the change was overwritten by future code in the method before the return statement. 

3. Replaced return value with null 

This mutation is created by pitest by replacing the return value of a method with null. For instance if range values are supposed to be returned from a method, it returns null instead. 

This mutant was killed in many instances in our original test suite beacuse of the assert statements that were written to check if the appropriate numerical values was returned for the range methods.  

4. Negated conditional 

This mutation is created when pitest modifies the source code to negate a condition statement. For instance if the the condition was if(upper < lower) it would be mutated to if(!(upper < lower)

In our original test suite this mutation was not killed for any methods because we did not have any branch coverage. To improve the mutation coverage we included tests that had branch coverage which in turn would catch these mutations for the methods we wrote the test for. 

5. Not equal to equal 

This mutation is created when pitest changes the "!=" operator to "==" operator or just removed the "!" operator if it is present in the source code. AN instance of this would be if(x!=0) being changed to if(x==0). 

In our original test suite this mutation was not killed for any methods because we did not have any branch coverage. To improve the mutation coverage we included tests that had branch coverage which in turn would catch these mutations for the methods we wrote the test for. 

6. Replaced double division with multipication

This mutant is created when pitest substitutes the division operator with the multiplication operator. For example x / 1.0 becomes x * 1.0. 

This mutation was killed in our original test suite for most methods because the return values were altered making the test cases able to catch them.

7. Lesser than to equal

This mutation is created by pitest when it changes the lesser than operator to the equality operator. For instance if(x < 5) becomes if (x == 5). 

In our original test suite this mutation was killed beacuse we had boundary coverage for all methods making the muatations detectable and be able to be killed.

8. Greater than to equal

This mutation is created by pitest when it changes the greater than operator to the equality operator. For instance if(x > 5) becomes if (x == 5). 

In our original test suite this mutation was killed beacuse we had boundary coverage for all methods making the muatations detectable and be able to be killed.

9. Replaced double division with modulus 

This mutation is created when pitest alters the source code by substituting the division operator with the modulus operator. For instance x / 2.0 becomes x % 2.0.

This mutation was killed in our original test suite for most methods because the return values were altered making the test cases able to catch them.

10. Replaced double division with addition 

This mutation is created when pitest alters the source code by substituting the division operator with the addition operator. For instance x / 2.0 becomes x + 2.0.

This mutation was killed in our original test suite for most methods because the return values were altered making the test cases able to catch them.

# Report all the statistics and the mutation score for each test class

<img width="1443" alt="Screenshot 2023-03-16 at 6 14 10 PM" src="https://user-images.githubusercontent.com/71629902/225974792-8dc7ae0c-9697-4fd8-bd97-9f439d38fabe.png">

<img width="870" alt="Screenshot 2023-03-17 at 8 08 18 AM" src="https://user-images.githubusercontent.com/71629902/225974816-aaf66afa-6438-4c56-be0c-ab242bcf3748.png">

<img width="739" alt="Screen Shot 2023-03-18 at 12 03 38 AM" src="https://user-images.githubusercontent.com/70219463/226088440-d70722d2-98a4-4da9-a8d1-e85e9010315c.png">

# Analysis drawn on the effectiveness of each of the test classes
When performing mutation testing we can look at the effectiveness scores of each test class as a way to grade how good our test cases were made. By looking at the percentage we know the ratio of mutants killed by the test suite in relation to the amount generated. In an ideal situation, we want as many of the created mutants to be killed by our test cases. In our case we designed test cases for the Data Utilities class which covered above the majority of created mutants. Where as for the Range class we were only able to cover a minority of the possible mutants created. From previous reviews we came to the concludion and found that are coverage for both classes is quite high, but here these results signify that the data utilities class is capable of catching mutants better than the Range class. Altogether this shows us that, even though there might be a good range of coverage for classes, there still can be the need for some test cases that can properly detect mutants(bugs). 

# A discussion on the effect of equivalent mutants on mutation score accuracy
We know that the mutation score is calculated as:
```
Mutation Score = (# of mutants killed by the test suite) 
                  -------------------------------------
                  (# of all non-equivalent mutants)
```

As an example, let's say we have 100 mutants:
50 of which are killed
25 of which are alive
25 of which are equivalent

Then by applying the formula above we get: 50/75 = 67% (mutation score)

As such, we see that equivalent mutants as discussed in lectures are a type of mutation that we want to avoid and it is not even considered as part of our mutation score. We then conclude that equivalent mutatns don't have impact on our mutation score accuracy as it is not taken into account when doing the calculation.

Detection of equivalent mutants is difficult because they are semantically equivalent to the original program and only really differ in terms of syntax. We believe that equivalent mutation detection may come in the form of seeing if our boundary-value testing can detect them or not because in some cases an equivalent mutant may be killed if it is tested against a test case which contains some form of boundary value. 

# A discussion of what could have been done to improve the mutation score of the test suites

We know that to increase our mutation score we need to kill more mutants overall within our test suite, as the formula below outlines. We also understood that there can be a very large combination of mutants and their types that can be generated using our tools so it would not be feasible to try generating many different mutants and trying to change or add test cases each and every time, which is why we've adopted a more refined design strategy.

```
Mutation Score = (# of mutants killed by the test suite) 
                  -------------------------------------
                  (# of all non-equivalent mutants)
```


Our design strategy involves firstly looking at the SUT to see where exactly there can be possible mutations and then looking at out existing test suite to see if theoretically it can kill the mutants or not. Once we've pointed out some areas of improvement, we go ahead and either change an existing test case or create a new test case to "kill" a potential mutation. After we have done this, we then test it against the generated mutants and by doing that we are able to increase our mutation score.

# Why do we need mutation testing? Advantages and disadvantages of mutation testing
We need mutation testing so see if our test suite can detect majority of the bugs, whereas with black-box and white-box testing that is primarily if it covers most of the specification (code/data). In essence, coverage testing does not ensure the quality of testing, it is a good measure of coverage criteria, which is why mutation testing is needed to stress test our suite against mutants.

Advantages of Mutation Testing:

Mutation testing can be automated and systematic - it is relatively easy to set up and also use with an effective mutation test tool. Mutation scores are also an excellent way of assessing the adequacy/quality of our test suite. The mutation score is essentially our "fault detection power", meaning that we can compare different suites and different techniques to see which of them yields us the best results.

Disadvantages of Mutation testing:

A more obvious disadvantage for mutation testing comes with equivalent mutants - mutants that are syntactially different but semantically produce the same result. We can see that the mutation score does not account for equivalent mutants either, and these are mutants that are much harder to kill comparatively. We have learned that equivalent mutation detection is in theory possible to do, but it is considered an "undecidable" problem. There can also be a case where we have a significantly large number of mutants which will require further resources.

# Explain your SELENUIM test case design process

Test cases were developed considering the most general functions of the website (Amazon) while including some less popular use cases to create a holisitic test suite. The functionalities that we determined to be most popular were log-in/log-off, searching and adding/deleting items to the cart, and changing the delivery address and preferred country site, with more niche cases including editing the bio of the logged in user.

The steps included in the test case avoided as many mouse-over commands as possible, as Selenium's recording process is not completely reliable and may overlook any mouse-over actions during the recording.

# Explain the use of assertions and checkpoints

Assertions (verify text/element) were used at the end of each test on an element that should be present at the end of every functionality that is tested. For example, when logging in onto Amazon, "Hello <Username>" will show on the top-right corner, and we use the verify text command to check if the test passed.

# how did you test each functionaity with different test data
  
The method on how each functionality is tested with different data is shown below:
- Login: use correct login information vs. incorrect data
- Logoff: N/A
- Search Item: search 2 different items
- Add Item to Cart: add 2 different items
- Change Address: use 2 different addresses
- Change Country: use 2 different countries
- Delete Item From Cart: N/A
- Change Profile Bio: use 2 different bio texts

# Discuss advantages and disadvantages of Selenium vs. Sikulix
Advantages of Selenium:

    Cross-platform compatibility: Selenium supports multiple programming languages and can be run on different operating systems like Windows, Mac, and Linux.
    Robust framework: Selenium provides a robust testing framework that can be used for different types of web applications.

Disadvantages of Selenium:

    Complex setup: Selenium requires a complex setup process, and it can take some time to configure.
    Limited support for desktop applications: Selenium is primarily used for web application testing and has limited support for desktop applications.

Advantages of SikuliX:

    Easy to use: SikuliX is easy to use, and testers can automate test cases using simple visual recognition.
    Image-based automation: SikuliX provides image recognition capabilities, allowing testers to automate scenarios that are difficult to automate using Selenium.

Disadvantages of SikuliX:

    Limited support for web applications: SikuliX is primarily used for desktop application testing and has limited support for web applications.
    Lack of cross-platform compatibility: SikuliX is only compatible with the Java platform and does not support other programming languages.

# How the team work/effort was divided and managed

The teamwork was divided between both the coding and report. We used pair-programming and paired up with one member telling the other the instructions to execute and having the other person execute those tools/commands. Split up the different test causes/suite amongst our two classes. For the report we split the different sections up amongst us.


# Difficulties encountered, challenges overcome, and lessons learned
The initial setup of the lab was difficult, as for some reason the tool kept showing errors so there was some initial debugging required on our end to get Pitest and other tools to work. Creating better test cases for mutation testing was also challenging, as we had to thoroughly look at our test suite for any weaknesses and try our best to come up with as big of a mutation score as possible. Overall, we learned that software testing would not be complete without mutation testing, and that web/GUI testing is an excellent way to test user/client-side interfaces.

# Comments/feedback on the lab itself
Instructions were easy to follow, so no comments or feedback from us.
