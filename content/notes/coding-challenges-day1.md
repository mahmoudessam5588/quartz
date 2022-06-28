---

title: "Coding Challenges Day One"
tags:
- Scala-Exercises

    
---

![MasterHead](https://st.depositphotos.com/1152339/2258/i/600/depositphotos_22588457-stock-photo-technology-concept-hex-code-digital.jpg)

## [GitHub Source Code](https://github.com/mahmoudessam5588/Scala-Coding_Challenge-DayOne)

## Problem One (Top K Frequent Elements)

  ![The Probem](https://images2.arabicprogrammer.com/409/ff/ff8e52dc7544efb1d48ef4f711653a49.png)

  ![The Problem 2](https://img-blog.csdnimg.cn/20200104164231783.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L09yaWVudGxpdTk2,size_16,color_FFFFFF,t_70)

  ### Understanding the problem

  1-First It's not an empty array sow we won't bother ourselves about (Options ,Some,Nil)
  2-Second Array in Scala in **Mutable** **indexed** **homogenous** type of collection,so what benefits an array brings  as a data structure _the elements in array can be accessed randomly by using the index number. Arrays allocate memory in contiguous memory locations for all its elements. Hence there is no chance of extra memory being allocated in case of arrays. This avoids memory overflow or shortage of memory in arrays so accessing an element is very easy For any reason a user wishes to store multiple values of similar type then the Array can be used and utilized efficiently which is the case in this example_
  3- Algorithm time complexity **Must Be** O(nlog(n))therefore, there must be something related to binary structures or divide & conquer.
  If you see this image Below you will find out that we are Dealing with some kind of **search** and/or **sorting By**
  ![image1](https://qph.fs.quoracdn.net/main-qimg-f8c3620e14dbaa97e8a35d51545f9da7.webp)
  4- Looking at given example it-self we have Two parameters `nums` Array of Int and `k` an Int is to be mapped or matched against `nums` if `k` equal value to most frequent elements or second most frequent element it's added to  `nums` as a second element else it's discarded also take in consideration that the elements inside `nums` may have negative numbers
  **without further ado** lest see the solution below and I will dissect it piece by piece with detailed explanation below the solution  

  ### The Solution Of The Problem

  ```scala
    def solve(nums: Array[Int], k: Int): Array[Int] =
       nums.groupBy(identity)
       .view.mapValues(_.length)
       .toArray.sortBy(_._2)
       .map(_._1).reverse.take(k)
  ```

  ### Explaining the Solution

  1- `groupBy` For grouping elements in a Scala collection by a provided key
  which has the following signature for an Iterable:

  ```scala
    // Method groupBy
    def groupBy[K](f: (A) => K): immutable.Map[K, Iterable[A]]
  ```

  It returns an immutable Map of elements each consisting of a key and a collection of values of the original type. To process this collection of values in the resulting Map, Scala provides a method `view.mapValues` with the below signature:

  ```scala
    // Method mapValues
    def mapValues[W](f: (V) => W): Map[K, W]
  ```

  This `groupBy/view.mapValues` combo proves to be handy for processing the values of the Map generated from the grouping.
  
  2- _What `identity` Means_ identity is a function By using identity, which is a "nice" way to say `x => x` we get a map where each Int gets separated in map, Like following:

  ```scala
    Map(1->Array(1,1,1),3->Array(3),2->Array(2,2))
  ```

  And here the method Signature:

  ```scala
    def identity[A](x : A) : A = { /* compiled code */ }
  ```

  3- What `_.length` Means in scala Placeholder syntax. Scala allows the use of underscores (denoted as ‘_’) to be used as placeholders for one or more parameters. we can consider the underscore to something that needs to be filled in with a value. However, each parameter must appear only one time within the function literal.
  Note: Internally, the underscore is expanded into a literal for a function that takes input as 1 parameter and then checks the condition which is mentioned. The same rule applies for more than 1 parameter. Multiple underscores means multiple parameters and not the use of same parameter repeatedly. Hence, this syntax is used when you want to take 1 or more parameters only once
  **In Our Case `_` here a short hand for single parameter anonymous function (x=>x)**
  **_Summarizing The Process Till now we mapped the `nums` Array as key value pairs of it's given element as key then we mapped the values of the map to their given length_**

  4-`toArray`  is used to convert the given **sortedMap as Mentioned Above** to an array. It stores the elements in a 2-D array in which each row consists of the key and value of the map.
  I won't go in details about the wrapping and implicits of toArray method it would be out of scope of this Article but follow my blog I'm Willing to explain all Scala concepts in the upcoming Articles

  5-`sortBy(_._2)`
  here is the method Signature:

  ```scala
   sortBy[B](f : scala.Function1[A, B])(implicit ord : scala.math.Ordering[B]) : scala.Array[A] = { /* compiled code */ }
  ```

  it takes two function parameters and return a sorted array **in our example we tell the function to take whatever
  and sort the second element of 2_D array
  according to natural ordering**

  6- `.map(_._1)` now after sorting it's time to transform this array according to  first element of 2-D Array
  7- `reverse.take(k)` before explaining why `reverse` method let me tell you about `take()` method,, the take() method is utilized to return a stack consisting of the first ‘n’ elements of the stack so it will return the head of the array which is most likely be the most frequent element in the array we done computing on so I reversed the list to let the take method return from the tail which is likely be the second most frequent element in the array

  **_All Thanks To [Eichorn](https://www.reddit.com/user/Eichhorn/) from scala Reddit community for his help for optimizing this solution the most way possible_**



## Problem Two (Contains Duplicates)
  ![problem3](https://kkminseok.github.io/assets/img/sample/leetcode/217/input.JPG)

  ### UnderStanding The Problem

  true if there is duplicates false if no duplicates  simple and easy return value of function boolean 

  ### The Solution Of The Problem

  ```scala
     nums.toSet.size != nums.length
  ``` 


  ### Explaining The Solution
  I tried sorting and recursion but I Wasn't As fast As the Solution Above 
  I was tempted to use imperative Programming Style using `for loop` with `var` and Mutable Collection for faster Times but I will Stick with functional programming way the idea here is compare between the `Int` of  two types of collections as we know that `Set` Collection doesn't allow/add duplicate elements so i use it to compare it with the length of the `nums` array


---
**_Thanks For Visiting And Reading My Articles Stay Tuned For Upcoming Articles_**    
