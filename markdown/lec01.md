### CS 131: Programming Languages
# Welcome to Programming Languages

## Course Information
### Professors
- Lucas Bang, "Prof. Bang" (he/him)
  - Interests: quantitative program analysis, programming, society, and culture, cold brew horchata coffee, singing dogs
- Ben Wiedermann, "Prof. Ben" (he/they)
  - Interests: programming language design + accessibility, programming, society, and culture, platypuses (platypi?)

## Course Mechanics
In this course, we emphasize **Flexibility, Community, and Certainty**. Here's an overview of how the course operates:
- All course materials, including videos, readings, and exercises, are available on Sakai.
- We follow a flipped classroom model where you engage with the course materials before the class session.
- Pair programming is encouraged to foster collaboration and learning from peers.
- We provide office and tutoring hours to address your questions and provide additional support.
- You will have weekly assignments that include completion-based exercises.
- A project and three quizzes will help you apply your knowledge.
- The course follows a highly structured and scaffolded schedule to ensure a smooth learning experience.

## Personal Item Sharing
As a way to get to know each other, take a moment to find a personal item that you want to share with the class. This can be a physical object or a picture on your device. In groups of 3 (or 2 or 4), introduce yourselves and share the item you brought. Explain why it is important to you. This activity aims to foster a sense of community and provide insights into each other's interests.

## A "Typical Week" in CS 131
To give you an idea of the course flow, here's a breakdown of a typical week in CS 131:
| Sunday                     | Monday                     | Tuesday | Wednesday                   | Thursday | Friday | Saturday |
|----------------------------|----------------------------|---------|-----------------------------|----------|--------|----------|
|                            |                            |         | Modules available<br>Flexible class<br>HW write-up available|          |        |          |
| Sub-module completion due <br>Previous assignment due| HW fully posted <br>In-class HW kickoff <br>Required Class |         | Sub-module completion due <br>Next Modules posted <br>Flexible class|          |        |          |
| **Current Assignment due**     |                            |         |                             |          |        |          |

And here are the deadlines and class format for a typical week: 

### Sunday
- Assignment due
- Sub-module completion due

### Monday
- In-class HW kickoff
- Required class

### Wednesday
- Sub-module completion due
- Flexible class

## Detailed Schedule
Throughout the semester, we follow a detailed schedule that outlines the topics, milestones, and assignments. This schedule helps you stay organized and manage your workload effectively. We will explore the schedule in more detail as we progress through the course, but for now, we will look at the schedule at a high-level.

![Course schedule](images/course_schedule.png)

We have structured the curriculum to provide a comprehensive understanding of fundamental programming language concepts while offering  opportunitites for individualized exploration. We refer to the initial phase of the course as "PLs Core." It covers essential topics that would be covered in most programming language classes. Following Spring Break, we reach a phase known as "Peak PLs," where we delve deeper into  concepts that may require a more significant mind stretch. This doesn't necessarily mean there will be more work, but there may be more mental investment needed. 

In designing this course, we've considered the workload you may have in other classes. As some other classes may be ramping up near the end of the semester, we transition to what might feel like a slightly relaxed pace, easing the mental stretch. This allows you to consolidate your knowledge and reflect on the concepts covered throughout the course.

At the culmination of the semester, we engage in final projects. These projects provide an opportunity for you to apply your skills and reinforce your understanding of programming languages. We offer flexibility in project selection, and a few intermediate deadlines will be set to help you stay on track and make steady progress. 

Overall, our aim is to provide a structured yet adaptable learning experience that fosters understanding, growth, and the development of programming language knowledge.

## What is a Programming Language?
In this exercise, take a moment to reflect on the definition of a programming language. Write a definition that you believe would be agreed upon by everyone. Alternatively, write a definition that you personally agree with but others may have differing opinions on. This exercise encourages critical thinking about the nature and purpose of programming languages.

## Module 1.1 on Sakai
To continue covering the remaining material from these slides, please complete Module 1.1 on Sakai. The module pages contain lecture videos and questions to reinforce your understanding. Regular participation and providing feedback help improve the learning experience for everyone.

## Upcoming Tasks
Here's a summary of the tasks to be completed this week:
- Complete the class participation/feedback form.
- Finish Module 1 by Sunday, 11:59 PM.
- Submit HW1 by Sunday, 11:59 PM.
- Fill out CS 131 intro survey to subit your GitHub ID.
- (optional but encouraged!) Attend Prof. Bang's office hours today from 5-6 PM in this room.
- On Monday, the HW2 kickoff will take place, along with a Haskell programming environment demo. We'll ensure everyone feels prepared and comfortable to start HW2 and Module 2.

## A Little History and Herstory (Theirstory?): 1830s-1840s
In this section, we explore the historical context of programming languages. We introduce Ada Lovelace (1815-1852), our "mathematician," and Charles Babbage (1791-1871), our "engineer." During the 1800s, the concept of a computer was different from what we understand today. "Computers" were people employed to perform complex calculations, such as logarithms, planetary motions, and trigonometric functions. Babbage realized that relying on humans for computations was prone to errors and tedious. This led to the development of mechanical machines for mathematical calculations. The combination of engineering and mathematics laid the foundation for modern computing.

Babbage, often referred to as the "father of the computer," designed early mechanical computing machines such as the Difference Engine and the Analytical Engine. The Difference Engine was a mechanical calculator that aimed to automate complex mathematical calculations. Babbage designed several versions of the machine, but it was never fully completed during his lifetime. The Analytical Engine was Babbage's most ambitious creation. It was an proposed general-purpose mechanical computer that had the ability to perform calculations, store data, and even execute conditional branching and loops. 

Ada Lovelace wrote an extensive set of notes on Babbage's Analytical Engine, which contained what is now recognized as the first published algorithm. Her notes described how the machine could be programmed to compute Bernoulli numbers; because of this, she could be considered the first computer programmer. Lovelace recognized that the Analytical Engine could go beyond mere arithmentic calculations and could be used to manipulate symbols. These insights into the Analytical Engine's capabilities foreshadowed the development of programming languages that would enable humans to interact with computers and instruct them to perform specific tasks.

## Math, Logic, and Western Philosophy Before 1900
Philosophers and mathematicians of the past, such as Gottfried Leibniz, George Boole, and John Locke, posed questions about the nature of knowledge, the laws of thought, and what can be known or proven. These inquiries set the stage for advancements in mathematics, logic, and the exploration of computation.

### What Can We Know and Prove?
The questions about knowledge and proof persisted. David Hilbert famously proclaimed, "We must know. We will know." However, Kurt Gödel's incompleteness theorem shattered the dream of a complete and consistent mathematical system. It demonstrated that there are true statements that cannot be proven within a given system.

### What Can We Compute?
Alan Turing and Alonzo Church made groundbreaking contributions to understanding computation. Turing proposed the idea of Turing Machines, simple theoretical devices capable of universal computation. Church developed the Lambda Calculus, a formal system for manipulating symbols that deals with functions. Both Turing Machines and Lambda Calculus contributed to our understanding of computation and the limits of what can be computed.

## Up and Down the Ladder of Abstraction
Programming languages exist on a spectrum of abstraction. At the lowest level, we have Turing Machines, which operate at the bit level and are highly stateful. As we move up the ladder of abstraction, we encounter higher-level languages, such as Assembly Language, imperative languages like C and C++ with manual memory management, higher-level languages like Python with no memory management, and functional languages like Racket, where functions are treated as data.

## Pure Functional Languages
Pure functional languages, like Haskell, go a step further in abstraction by eliminating mutable state entirely. In these languages, computations are expressed solely through the evaluation of functions, leading to elegant and concise code. Understanding pure functional languages broadens our perspective on programming paradigms.

## Why Functional Programming?
Functional programming offers several advantages. It eliminates the complexities of managing mutable state, provides a new way of thinking about computation, complements knowledge of other paradigms, and finds applications in correctness-crucial domains like security and finance. Many languages, including C++, Java, and Python, are incorporating functional features, making it a valuable skill for programmers.

## Topics in CS 131
Throughout this course, we will cover various topics that explore the depth and breadth of programming languages:
- Functional Programming: Emphasizing the role of functions as data and the evaluation of expressions.
- Pattern Matching: Leveraging the structure of data to simplify programming.
- Representing Data: Exploring data structures from a functional perspective.
- Parsing: Transforming characters into executable programs.
- Interpreters: Understanding the process of turning programs into computation.
- Abstraction: Doing more with less code through abstraction techniques.
- Types: Examining the role of types in computing the right "kind" of information.
- Lambda Calculus: Investigating the fundamental model of computation through lambda calculus.
- Social and Cultural Implications: Considering the impact of programming languages on society and culture.
- Your Ideas: Encouraging your creativity and exploration of programming language concepts.

## Programming Languages by People, for People
While programming languages are ultimately designed by people, they significantly influence our thinking, problem-solving approaches, and solution development. Each programming language carries the perspectives and intentions of its creators. Understanding the people behind programming languages enhances our appreciation for their design choices and the diverse landscape of languages available today.

## Conclusion
Programming languages are powerful tools for expressing computations and solving problems. In CS 131, we aim to explore the fundamental principles and concepts that underpin programming languages. By understanding these principles and becoming proficient in functional programming, we can become more effective programmers, capable of leveraging the strengths of different languages and approaching problems from diverse perspectives.