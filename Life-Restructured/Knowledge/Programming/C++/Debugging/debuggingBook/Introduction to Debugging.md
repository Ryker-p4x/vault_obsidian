The typical debugging situation is something like this:
1. A program is being ran
2. The output from the program is in error
3. The input is assumed to be correct
If the input were to be incorrect, we wouldn't be searching on the output, but instead on what produced the input. If it's from a third party, then you should just reject the input if it's incorrect.

This situation can be seen as:
![[Pasted image 20261012150631.png|350]]

If we were to break down the program into several states this is what it'd look like:
![[Pasted image 20261012150659.png]]

Initially it's correct but on state 2 it seems to break due to whatever defect's occurring.

A fault like this comes to be from steps in the program code, which take a state as input and output another state.

So what's happening on the second image is that state 2 receives a correct output and outputs a wrongful one which propagates to the next state and to the final output.

The goal of debugging is to find this step where the state that gets outputted is wrong.

However, this isn't easy because of program state, let's say we have 3 vars:

![[Pasted image 20261012150922.png]]

Var 2 gets a wrongful output and that propagates to everything.
This is called a *cause-effect* chain.
- The faulty variable causes a fault on the state's entirety.
- The fault in the state propagates to the next execution steps until it becomes visible as a failure

Sometimes, the code can even take the wrong logic path instead of calculating a wrong number which is much harder to detect. Something like that can be generally much harder to find.

Since the code was written by a human, any defect can be related to some mistake from the programmer. So with this knowledge: 
- A mistake is a human act or decision resulting in an error on the program
- A defect is the error in the program code. Also called bug.
- A fault is an error in the program state. Also called infection.
- A failure is an externally visible error in the program behavior. Also called malfunction.

### From failure to defect:

To find a defect from a failure, we trace back the faults along their propagation. We start from the very end of the execution and then gradually progress back in time, examining fault by fault until we find a transition from a correct state to a faulty state. A step in which correct state comes in and faulty state comes out. 

This sounds like a straightforward strategy, however it doesn't always work in practice:
- First, program states are large, searching thousands of values and check each one for faults, you'll spend LOTS of time on one single state.
- You don't always know whether a state is correct or not. There's not always some specification to the expected results of an intermediate state. If one had one that could check each state for correctness, debugging would be easy and of little importance.
- Third, executions don't come in a handful of steps, they can easily be thousands to millions of steps. Which means you won't have to examine one state, but several, making the problem much worse.
To make your search efficient, start with the most likely causes, then gradually go to the least likely ones. This is what we call a *debugging strategy*. Intermediate assertions of the program can also come in handy. As they make the cause-effect chain smaller

The scientific method to find causes of something goes as follows:
1. Formulate a question, such as "why does the apple fall down?"
2. Invent a *hypothesis* based on knowledge obtained while formulating the question, that could explain the observed behavior.
3. Based on the logical consequences of your hypothesis, formulate a prediction that can support or neglect the hypothesis. Ideally the prediction would distinguish the hypothesis from likely alternatives.
4. Conduct experiments for your prediction. If the prediction holds, confidence in your hypothesis may increase; otherwise, it decreases.
5. Repeat steps 2-4 until there are no discrepancies between hypothesis and predictions and/or observations.

At this point, your hypothesis should become a theory, a predictive and comprehensive description of some aspect of the natural world.

Our debugging problems, would require of a theory on how the failure came out to be, but the process is pretty much the same.

![[Pasted image 20261012160556.png]]


You should only fix your code after having a diagnosis which should explain two things:
- Why and how did the failure ocur?
- How is the code incorrect?

Showing both these aspects requirements – _causality_ and _incorrectness_ – are crucial for a debugging diagnosis:

- If you find that you can change some location to make the failure go away, but are not sure why this location is wrong, then your "fix" may apply only to the symptom rather than the source. Your diagnosis explains _causality_, but not _incorrectness_.
- If you find that there is a defect in some code location, but do not verify whether this defect is related to the failure in question, then your "fix" may not address the failure. Your diagnosis addresses _incorrectness_, but not _causality_.

You can become a better debugger by
	1- Following a systematic process like the scientific method
    - Keeping a log of your observations and hypotheses
    - Making your observations and conclusions explicit by telling them somebody (or something).