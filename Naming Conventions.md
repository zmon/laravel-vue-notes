
From Stack Exchange:

# [How can we teach good naming practice for students learning Java?](https://cseducators.stackexchange.com/questions/4594/how-can-we-teach-good-naming-practice-for-students-learning-java)

The following is from the above:

### What works
I have found that the following question is a useful overriding guide for most of my students:

"If you were not someone who had just spent the last 15 hours looking over this code in detail, what are the odds that you could figure out what it was doing at a quick glance?"

### Naming norms
This is the best tool that I use, and these work for all of my students. There are a few direct practices that I ask for in all submitted code:

* With regard to booleans, what do we know if this variable is true? Create a name based on the true condition. (e.g. if this variable will be true whenever the foo is inside the bar, we would name the variable fooInBar)
* With regards to accessor methods, what information is being returning? Simply name this information. (totalTrials(), unusedElements(), nextItem(), etc.)
* With regards to mutators, what command (verb) is being issued? Use this verb, possibly with an attached noun. (increment(), consume(Item i), fixVertex(), etc.)
* Single letter variable names should be used only for throwaway counters and such. (e.g. for(int k = 0; k < items.length(); k++))
* For other variables, we enter into broader territory, and things can get trickier. Which brings us to...

### Miscellaneous variables
Unintuitively, I have had mixed luck with the question,

"what does this variable actually represent?"

This is the question that I ask myself while I code, and it works for many students, but for students who really struggle to come up with good names, the question does not seem to grant much insight.

This doesn't mean that I don't use the question, but it has become a last resort. Students who present poorly named variables often seem unable to cleanly articulate what a particular variable is accomplishing.

If I'm honest, the fact that this question rarely helps strugglers makes little sense to me (and is rather disheartening), but I have come to accept it as a fact. Going back to my intuition that strong writers create clean code, there could be some language difficulty going on here, but that is only a hunch.

For such strugglers, I might help them by having them describe the variable in broad terms, and writing what they say. I will then sit and progressively distill what they have written with them until we arrive at a good name together. Unfortunately, this practice is time intensive and does not scale well, but it works, and I haven't found any better solutions for my strugglers.