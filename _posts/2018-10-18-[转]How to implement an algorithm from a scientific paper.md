---
layout: post
title: [转]How to implement an algorithm from a scientific paper
tags:
  - Notes
---

This article is a short guide to implementing an algorithm from a scientific paper. I have implemented many complex algorithms from books and scientific publications, and this article sums up what I have learned while searching, reading, coding and debugging. This is obviously limited to publications in domains related to the field of Computer Science. Nevertheless, you should be able to apply the guidelines and good practices presented below to any kind of paper or implementation.

To receive a notification email every time a new article is posted on Code Capsule, you can subscribe to the newsletter by filling up the form at the top right corner of the blog.
As usual, comments are open at the bottom of this post, and I am always happy to welcome questions, corrections and contributions!

## 1 – Before you jump in

There are a few points you should review before you jump into reading a technical paper and implementing it. Make sure you cover them carefully each time you are about to start working on such a project.

### 1.1 – Find an open source implementation to avoid coding it

Unless you want to implement the paper for the purpose of learning more about the field, you have no need to implement it. Indeed, what you want is not coding the paper, but just the code that implements the paper. So before you start anything, you should spend a couple of days trying to find an open source implementation on the internet. Just think about it: would you rather lose two days looking for the code, or waste two months implementing an algorithm that was already available?

### 1.2 – Find simpler ways to achieve your goal

Ask yourself what you are trying to do, and if simpler solutions would work for what you need. Could you use another technique – even if the result is only 80% of what you want – that does not require to implement the paper, and that you could get running within the next two days or so with available open source libraries? For more regarding this, see my article [The 20 / 80 Productivity Rule](http://codecapsule.com/2011/03/06/20-80-productivity-rule/).

### 1.3 – Beware of software patents

If you are in the U.S., beware of software patents. Some papers are patented and you could get into trouble for using them in commercial applications.

### 1.4 – Learn more about the field of the paper

If you are reading a paper about the use of Support Vector Machines (SVM) in the context of Computational Neuroscience, then you should read a short introduction to Machine Learning and the different types of classifiers that could be alternatives to SVM, and you should as well read general articles about Computational Neuroscience to know what is being done in research right now.

### 1.5 – Stay motivated

If you have never implemented a paper and/or if you are new to the domain of the paper, then the reading can be very difficult. Whatever happens, do not let the amount and the complexity of the mathematical equations discourage you. Moreover, speed is not an issue: even if you feel that you understand the paper slower than you wish you would, just keep on working, and you will see that you will slowly and steadily understand the concepts presented in the paper, and pass all difficulties one after the other.

## 2 – Three kinds of papers

It is never a good idea to pick a random paper and start implementing in right away. There are a lot of papers out there, which means there is a lot of garbage. All publications can fit into three categories:

### 2.1 – The groundbreaking paper

Some really interesting, well-written, and original research. Most of these papers are coming out of top-tier universities, or out of research teams in smaller universities that have been tackling the problem for about six to ten years. The later is easy to spot: they reference their own publications in the papers, showing that they have been on the problem for some time now, and that they base their new work on a proven record of publications. Also, the groundbreaking papers are generally published in the best journals in the field.

### 2.2 – The copycat paper

Some research group that is just following the work of the groundbreaking teams, proposing improvements to it, and publishing their results of the improvements. Many of these papers lack proper statistical analysis and wrongly conclude that the improvements are really beating the original algorithm. Most of the time, they really are not bringing anything except for unnecessary additional complexity. But not all copycats are bad. Some are good, but it’s rare.

### 2.3 – The garbage paper

Some researchers really don’t know what they are doing and/or are evil. They just try to maintain their status and privileges in the academic institution at which they teach. So they need funding, and for that they need to publish, something, anything. The honest ones will tell you in the conclusion that they failed and that the results are accurate only N% of the time (with N being a bad value). But some evil ones will lie, and say that their research was a great success. After some time reading publications, it becomes easy to spot the garbage paper and ditch them.

## 3 – How to read a scientific paper

A lot has already been written on the topic, so I am not going to write much about it. A good starting point is: *How to Read a Paper* by Srinivasan Keshav. Below are a few points that I found useful while I was reading scientific publications.

### 3.1 – Find the right paper

What you want to implement is an original paper, one that started a whole domain. It is sometimes okay to pick a copycat paper, if you feel that it brings real improvements and consistency to a good but immature groundbreaking paper.

So let’s say you have a paper as your starting point. You need to do some research in its surroundings. For that, the strategy is to look for related publications, and for the publications being listed in the “References” section at the end of the paper. Go on [Google Scholar](http://scholar.google.com/) and search for the titles and the authors. Does any of the papers you found do a better job than the paper you had originally? If yes, then just ditch the paper you were looking at in the first place, and keep the new one you found. Another cool feature of Google Scholar is that you can find papers that cite a given paper. This is really great, because all you have to do is to follow the chain of citations from one paper to the next, and you will find the most recent papers in the field. Finding the good paper from a starting point is all about looking for papers *being cited* by the current paper, and for papers *citing* the current paper. By moving back and forth in time you should find the paper that is both of high quality and fits your needs.

Important: note that at this stage of simple exploration and reckoning, you should not be reading and fully understand the papers. This search for the right paper should be done just by skimming over the papers and using your instinct to detect the garbage (this comes with experience).

### 3.2 – Do not read on the screen

Print the publication on hard paper and read the paper version. Also, do not reduce the size in order to print more on each page. Yes, you will save three sheets of paper, but you will lose time as you will get tired faster reading these tiny characters. Good font size for reading is between 11 and 13 points.

### 3.3 – Good timing and location

Do not read a paper in the middle of the night, do it at a moment of the day when your brain is still fresh. Also, find a quiet area, and use good lighting. When I read, I have a desk lamp pointing directly at the document.

### 3.4 – Marker and notes

Highlight the important information with a marker, and take notes in the margin of whatever idea that pops in your head as you read.

### 3.5 – Know the definitions of all the terms

When you are used to read mostly news articles and fiction, your brain is trained to fill-in meaning for words that you do not know, by using context as a deduction device. Reading scientific publications is a different exercise, and one of the biggest mistake is to assume false meaning for a word. For instance in this sentence “The results of this segmentation approach still suffer from blurring artifacts”. Here two words, “segmentation”, and “artifacts”, have a general meaning in English, but also have a particular meaning in the domain of Computer Vision. If you do not know that these words have a particular meaning in this paper, then while reading without paying attention, your brain will fill-in the general meaning, and you might be missing some very important information. Therefore you must (i) avoid assumptions about words, and whenever in doubt look up the word in the context of the domain the publication was written, and (ii) write a glossary on a piece of paper of all the concepts and vocabulary specific to the publication that you did not know before. If you encounter for the first time concepts such as “faducial points” and “piece-wise affine transform”, then you should look-up their precise definitions and write them down in your glossary. Concepts are language-enabled brain shortcuts, and allow you to understand the intent of the authors faster.

### 3.6 – Look for statistical analysis in the conclusion

If the authors present only one curve from their algorithm and one curve from another algorithm, and say “look, it’s 20% more accurate”, then you know you’re reading garbage. What you want to read is: “Over a testing set of N instances, our algorithm shows significant improvement with a p-value of 5% using a two-sample t-test.” The use of statistical analysis shows a minimum of driving from the author, and is a good proof that the results can be trusted for generalization (unless the authors lied to make their results look more sexy, which can always happen).

### 3.7 – Make sure the conclusions are demonstrating that the paper is doing what you need

Let’s say you want an algorithm that can find any face in a picture. The authors of the paper say in the conclusion that their model was trained using 10 poses from 80 different people (10 x 80 = 800 pictures), and that the accuracy of face detection with the training set was 98%, but was only 70% with the testing set (picture not used during training). What does this mean? This means that apparently, the algorithm has issues to generalize properly. It performs well when used on the training set (which is useless), and perform worse when used in real-world cases. What you should conclude at this point is that maybe, this paper is not good enough for what you need.

### 3.8 – Pay attention to the input data used by the authors

If you want to perform face detection with a webcam, and the authors have used pictures taken with a high-definition camera, then there are chances that the algorithm will not perform as well in your case as it did for the authors. Make sure that the algorithm was tested on data similar to yours or you will end up with a great implementation that is completely unusable in your real-world setup.

### 3.9 – Authors are humans

The authors are humans, and therefore they make mistakes. Do not assume that the authors are absolutely right, and in case an equation is really hard to understand or follow, you should ask yourself whether or not the authors made a mistake there. This could just be a typo in the paper, or an error in the maths. Either case, the best way to find out is to roll out the equations yourself, and try to verify their results.

### 3.10 – Understand the variables and operators

The main task during the implementation of a publication is the translation of math equations in the paper into code and data. This means that before jumping into the code, you must understand 100% of the equations and processes on these equations. For instance, “C = A . B” could have different meaning. A and B could be simple numbers, and the “.” operator could simply be a product. In that case, C would be the product of two numbers A and B. But maybe that A and B are matrices, and that “.” represents the matrix product operator. In that case, C would be the product matrix of the matrices A and B. Yet another possibility is that A and B are matrices and that “.” is the term-by-term product operator. In that case, each element C(i,j) is the product of A(i,j) and B(i,j). Notations for variables and operators can change from one mathematical convention to another, and from one research group to another. Make sure you know what each variable is (scalar, vector, matrix or something else), and what every operator is doing on these variables.

### 3.11 – Understand the data flow

A paper is a succession of equations. Before you start coding, you must know how you will plug the output of equation N into the input of equation N+1.

## 4 – Prototyping

Once you have read and understood the paper, it’s time to create a prototype. This is a very important step and avoiding it can result in wasted time and resources. Implementing a complex algorithm in languages such as C, C++ or Java can be very time consuming. And even if you have some confidence in the paper and think the algorithm will work, there is still a chance that it won’t work at all. So you want to be able to code it as quickly as possible in the dirtiest way, just to check that it’s actually working.

### 4.1 – Prototyping solutions

The best solution for that is to use a higher level versatile language or environment such as Matlab, R, Octave or SciPy/NumPy. It is not that easy to represent a mathematical equation in C++ and then print the results to manually check them. On the contrary, it is extremely straightforward to write equations in Matlab, and then print them. What would take you two to three weeks in C++ will take take you two days in Matlab.

### 4.2 – Prototyping helps the debugging process

An advantage of having a prototype is that when you will have your C++ version, you will be able to debug by comparing the results between the Matlab prototype and the C++ implementation. This will be developed further in the “Debugging” section below.

### 4.3 – Wash-off implementation issues beforehand

You will certainly make software design mistakes in your prototype, and this is a good thing as you will be able to identify where are the difficulties with both the processes or data. When you will code the C++ version, you will know how to better architect the software, and you will produce way cleaner and more stable code than you would have without the prototyping step (this is the “throw-away system” idea presented by Frederick Brooks in [The Mythical Man-Month](http://en.wikipedia.org/wiki/The_Mythical_Man-Month)).

### 4.4 – Verify the results presented in the paper

Read the “Experiment” section of the paper carefully, and try to reproduce the experimental conditions as closely as possible, by using test data as similar as possible to the ones used by the authors. This increases your chances of reproducing the results obtained by the authors. Not using similar conditions can lead you to a behavior of your implementation that you might consider as an error, whereas you are just not feeding it with the correct data. As soon as you can reproduce the results based on similar data, then you can start testing it on different kinds of data.

## 5 – Choose the right language and libraries

At this stage, you must have a clear understanding of the algorithm and concepts presented in the publication, and you must have a running prototype which convinces that the algorithm is actually working on the input data you wish to use in production. It is now time to go into the next step, which consists in implementing the publication with the language and framework that you wish to use in production.

### 5.1 – Pre-existing systems

Many times, the production language and libraries are being dictated by pre-existing systems. For instance, you have a set of algorithm for illumination normalization in a picture, in a library coded in Java, and you want to add a new algorithm from a publication. In that case, obviously, you are not going to code this new algorithm in C++, but in Java.

### 5.2 – Predicted future uses of the implementation

In the case there is no pre-existing system imposing you a language, then the choice of the language should be done based upon the predicted uses of the algorithm. For example, if you believe that within four to six months, a possible port of your application will be done to the iPhone, then you should choose C/C++ over Java as it would be the only way to easily integrate the code into an Objective-C application without having to start everything from scratch.

### 5.3 – Available libraries that solve fully or partly the algorithm

The available libraries in different languages can also orient the choice of the production language. Let’s imagine that the algorithm you wish to implement makes use of well-known algebra techniques such as principal component analysis (PCA) and singular value decomposition (SVD). Then you could either code PCA and SVD from scratch, and if there is a bug could end up debugging for a week, or you could re-use a library that already implements these techniques and write the code of your implementation using the convention and Matrix class of this library. Ideally, you should be able to decompose your implementation into sub-tasks, and try to find libraries that already implement as many of these sub-tasks as possible. If you find the perfect set of libraries that are only available for a given language, then you should pick that language. Also, note that the choice of libraries should be a trade-off between re-using existing code and minimizing dependencies. Yes, it is good to have code for every sub-task needed for your implementation, but if that requires to create dependencies over 20 different libraries, then it might be not very practical and can even endanger the future stability of your implementation.

## 6 – Implementation

Here are some tips from my experience in implementing publications

### 6.1 – Choose the right precision

The type you will use for your computation should be chosen carefully. It is generally way better to use *double* instead of *float*. The memory usage can be larger, but the precision in the calculation will greatly improve, and is generally worth it. Also, you should be aware of the differences between 32-bit and 64-bit systems. Whenever you can, create your own type to encapsulate the underlying type (float or double, 32-bit or 64-bit), and use this type in your code. This can be done with a define is C/C++ or a class in Java.

### 6.2 – Document everything

Although it is true that over-documenting can slow down a project dramatically, in the case of the implementation of a complex technical paper, you want to comment everything. Even if you are the only person working on the project, you should document your files, classes and methods. Pick a convention like Doxygen or reStructuredText, and stick to it. Later in the development, there will be a moment where you will forget how some class works, or how you implemented some method, and you will thank yourself for documenting the code!

### 6.3 – Add references to the paper in your code

For every equation from the paper that you implement, you need to add a comment citing the paper (authors and year) and either the paragraph number or the equation number. That way, when later re-reading the code, you will be able to connect directly the code to precise locations in the paper. These comments should look like:

```
// See Cootes et al., 2001, Equation 2.3// See Matthews and Baker, 2004, Section 4.1.2
```

### 6.4 – Avoid mathematical notations in your variable names

Let’s say that some quantity in the algorithm is a matrix denoted A. Later, the algorithm requires the gradient of the matrix over the two dimensions, denoted dA = (dA/dx, dA/dy). Then the name of the the variables should not be “dA_dx” and “dA_dy”, but “gradient_x” and “gradient_y”. Similarly, if an equation system requires a convergence test, then the variables should not be “prev_dA_dx” and “dA_dx”, but “error_previous” and “error_current”. Always name things for what physical quantity they represent, not whatever letter notation the authors of the paper used (e.g. “gradient_x” and not “dA_dx”), and always express the more specific to the less specific from left to right (e.g. “gradient_x” and not “x_gradient”).

### 6.5 – Do not optimize during the first pass

Leave all the optimization for later. As you can never be absolutely certain which part of your code will require optimization. Every time you see a possible optimization, add a comment and explain in a couple of lines how the optimization should be implemented, such as:

```
// OPTIMIZE HERE: computing the matrix one column at a time// and multiplying them directly could save memory
```

That way, you can later find all the locations in your code at which optimizations are possible, and you get fresh tips on how to optimize. Once your implementation will be done, you will be able to find where to optimize by running a profiler such as Valgrind or whatever is available in the programming language you use.

### 6.6 – Planning on creating an API?

If you plan on using your current code as a basis for an API that will grow with time, then you should be aware of techniques to create interfaces that are actually usable. For this, I would recommend the “coding against the library” technique, summarized by Joshua Bloch in his presentation [How to Design a Good API and Why it Matters](http://www.infoq.com/presentations/effective-api-design).

## 7 – Debugging

Implementing a new algorithm is like cooking a dish you never ate before. Even if it tastes kind of good, you will never know if this is what it was supposed to taste. Now we are lucky, since unlike for cooking, software development has some helpful trick to increase the confidence we have in an implementation.

### 7.1 – Compare results with other implementations

A good way to wash out the bugs is to compare the results of your code with the results of an existing implementation of the same algorithm. As I assume that you did correctly all the tasks in the “But before you jump” section presented above, you did not find any available implementation of the algorithm (or else you would have used it instead of implementing the paper!). As a consequence, the only other implementation that you have at this stage is the prototype that you programmed earlier.

The idea is therefore to compare the results of the prototype and the production implementation at every step of the algorithm. If the results are different, then one of the two implementations is doing something wrong, and you must find which and why. Precision can change (the prototype can give you x = 1.8966 and the production code x = 1.8965), and the comparison should of course take this into account.

### 7.2 – Talk with people who have read the paper

Once all the steps for both implementations (prototype and production) are giving the exact same results, you can gain some confidence that your code is bug free. However, there is still a risk that you made a mistake in your understanding of the paper. In that case, both implementations will give the same results for each step, and you will think that your implementations are good, whereas this just proves that both implementations are equally wrong. Unfortunately, there is no way that I know of to detect this kind of problems. Your best option is to find someone who has read the paper, and ask that person questions regarding the parts of the algorithm you are not sure about. You could even try to ask the authors, but your chances to get an answer are very low.

### 7.3 – Visualize your variables

While developing, it is always good to keep an eye on the content of the variables used by the algorithm. I am not talking about merely printing all the values in the matrices and data you have, but finding the visualization trick adapted to any variable in your implementation. For instance, if a matrix is suppose to represent the gradient of an image, then during the coding and debugging, you should have a window popping up and showing that gradient image, not just the number values in the image matrix. That way, you will associate actual an image with the data you are handling, and you will be capable of detecting when there is a problem with one of the variables, which in turn will indicate a possible bug. Inventive visualization tricks include images, scatter plots, graphs, or anything that is not just a stupid list of 1,000 numbers and upon which you can associate a mental image.

### 7.4 – Testing dataset

Generating data to experiment with your implementation can be very time consuming. Whenever you can, try to find databases (face database, text extract databases, etc.) or tools for generating such data. If there are none, then do not lose time generating 1000 samples manually. Code a quick data generator in 20 lines and get done with it.

## Conclusion

In this article, I have presented good practices for the implementation of a scientific publication. Remember that these are only based on my personal experience, and that they should not be blindly followed word for word. Always pay attention when you read and code, and use your judgement to determine which of the guidelines presented above fit your project. Maybe some of the practices will hurt your project more than it will help it, and that’s up to you to find out.

Now go implement some cool algorithm!



by Emmanuel Goossaert from http://codecapsule.com/2012/01/18/how-to-implement-a-paper/