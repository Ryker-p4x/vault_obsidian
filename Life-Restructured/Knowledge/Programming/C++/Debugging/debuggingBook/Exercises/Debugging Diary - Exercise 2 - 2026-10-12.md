## Symptom
<What did I observe? Exact command, exact output, which test failed.>
I observed that the order test fails
## Hypothesis
<One sentence: what I believe is wrong and where. Make it falsifiable.>
I believe that     return sorted(tasks, key=lambda t: (t["priority"], t["due"]), reverse=True)
in this line the reverse=True is making it get sorted by the highest priority but also the latest date instead of the earliest.

## Experiment
<What I changed/ran to test the hypothesis. Input used, before/after outputs.>
instead of changing the whole tuple I'm gonna do this: 
    return sorted(tasks, key=lambda t: (-t["priority"], t["due"]))
which should fix it

## Result
<Did the output confirm or contradict the hypothesis? New facts learned.>
I mean yeah the first test easily confirms my hypothesis already since it's a test based on the latest and earliest order

## Root cause
<The actual defect, stated as a mechanism (not just "line 42 is wrong").>
The defect is the fact that you're sorting by the latest date not the earliest.

## Fix
<The change made, and the test(s) that now pass.>
return sorted(tasks, key=lambda t: (-t["priority"], t["due"])) all tests pass now.

## How I'd find it faster next time
<The technique/shortcut that would have narrowed this fastest.>
I found it in like 3 mins so I don't think I could've been any faster.