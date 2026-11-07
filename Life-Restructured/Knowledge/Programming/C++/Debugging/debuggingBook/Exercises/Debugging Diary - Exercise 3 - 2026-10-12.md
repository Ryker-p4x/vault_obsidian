## Symptom
<What did I observe? Exact command, exact output, which test failed.>
I observed that AssertionError: Lists differ: [[1, 3]] != [[1, 10]] this test in specific failed. So I looked into the merge_intervals function and I noticed that all the other tests would work except this one. 
## Hypothesis
<One sentence: what I believe is wrong and where. Make it falsifiable.>
What the program was doing wrong is that it was merging the intervals and making last[1] to end even thought end was lower than last[1] which would shrink it.

## Experiment
<What I changed/ran to test the hypothesis. Input used, before/after outputs.>
Nothing to change or test since it's very intuitive and needed no confirmation.

## Result
<Did the output confirm or contradict the hypothesis? New facts learned.>
Nothing to confirm since it was very intuitive.

## Root cause
<The actual defect, stated as a mechanism (not just "line 42 is wrong").>
The defect was exactly what I put as my hypothesis.

## Fix
<The change made, and the test(s) that now pass.>
I modified one line of code only. Whenever last[1] would get modified it would do a max(end, last[1]) so that if end was lower than last[1] it wouldn't get wrongly defined.

## How I'd find it faster next time
<The technique/shortcut that would have narrowed this fastest.>
I took a really long time just thinking and thinking, next time I gotta try to understand the problem faster by either understanding what's trying to get achieved quicker or noticing patterns.