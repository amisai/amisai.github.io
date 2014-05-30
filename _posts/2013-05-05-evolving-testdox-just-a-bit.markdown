---
layout: post
title: "Evolving testdox just a bit"
date: 2013-05-05 12:56
comments: true
categories: [development]
---

A while ago, when learning about BDD, I found some references to agiledox (see, for instance in [Introducing BDD](http://dannorth.net/introducing-bdd/) of famous Dan North). 

As Dan Norh said: "My first “Aha!” moment occurred as I was being shown a deceptively simple utility called [agiledox](http://agiledox.sourceforge.net/), written by my colleague, Chris Stevenson. It takes a JUnit test class and prints out the method names as plain sentences ... The word “test” is stripped from both the class name and the method names, and the camel-case method name is converted into regular text. That’s all it does, but its effect is amazing." 

So, if you have a test case such as:
```
public class CustomerLookupTest extends TestCase {
    testFindsCustomerById() {
        ...
    }
    testFailsForDuplicateCustomers() {
        ...
    }
    ...
}
```

agiledox would render something like this:

```
CustomerLookup
- finds customer by id
- fails for duplicate customers
- ...  
```
This little tool helps you to learn about a class responsabilities in a automated way. As North said, this format led him to think about vocabulary we use while describing tests in TDD and provided him a solid ground to develop BDD.

As in $JOB we're using Java as primary language, with maven as project definition language, I've looking for a tool similar to agiledox to put in our building process. I've found [testdox](http://en.wikipedia.org/wiki/TestDox), with a maven plugin [here](https://github.com/wireframe/testdox-maven-plugin). This plugin iterates through all your tests and generates a site page with a list similar as rendered above. 

My main problem with that plugin is that we don't use [JUnit](http://junit.org/) but [TestNG](http://testng.org/), and we've evolved our tests naming from something like "testDoThis" to "shouldHappenThis". So I've forked that maven plugin in my own repository: [testdox-maven-plugin](https://github.com/amisai/testdox-maven-plugin) in order to adjust to new prefixes. We're keeping "should" prefix in responsabilities list, as it fits better for us, but maybe you want to change that. 

