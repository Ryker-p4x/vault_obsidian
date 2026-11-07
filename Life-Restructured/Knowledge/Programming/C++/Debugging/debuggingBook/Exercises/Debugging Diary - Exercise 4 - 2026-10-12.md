## Symptom
<What did I observe? Exact command, exact output, which test failed.>
I observed how only one test fails when running the get command which is         self.assertEqual(cache.get("b"), 20).
## Hypothesis
<One sentence: what I believe is wrong and where. Make it falsifiable.>
I believe that the problem is that the put command is wrongfully handling duplicates of values. Hm, I am wrong, after some rethinking I've noticed that it's reaching the limit and not adding the last value probably. This is due to the put function first trying to add the key instead of first removing extra keys. Nope all wrong, the true reason was that it wasn't moving the key to the end as recently used which made it get deleted as the last one.

## Experiment
<What I changed/ran to test the hypothesis. Input used, before/after outputs.>
I changed the code and saw how all my hypotheses failed until I reached the right one.

## Result
<Did the output confirm or contradict the hypothesis? New facts learned.>
The output denied the hypothesis 2 times until I got the right one at the end. I learned about LRU.

## Root cause
<The actual defect, stated as a mechanism (not just "line 42 is wrong").>
The actual defect was that the put function wasn't setting the newly made key as the most recent one.

## Fix
<The change made, and the test(s) that now pass.>
At the end of the put function i simply added a new line outside of the if statements:
self.data.move_to_end(key)

## How I'd find it faster next time
<The technique/shortcut that would have narrowed this fastest.>
Probably pay attention to what the functions are actually supposed to do and those comments since because I didn't pay attention I didn't notice it as quickly as I could have.