## Symptom
<What did I observe? Exact command, exact output, which test failed.>
I observed how a test would return the wrong accuracy. The test that failed was:
FAIL: test_accuracy_perfect (__main__.TestTypingStats.test_accuracy_perfect)
Traceback (most recent call last):
  File "/home/adrii/Work/scratch/debugging_practice/debuggingbook/debugging_exercises/test_exercise1.py", line 22, in test_accura
cy_perfect
    self.assertEqual(accuracy("hello world", "hello world"), 100.0)
    ~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
AssertionError: 90.91 != 100.0

## Hypothesis
<One sentence: what I believe is wrong and where. Make it falsifiable.>
The matching characters function was wrong. The part that's wrong is the len(expected) - 1 for the for loop. Since that skips the last member.

## Experiment
<What I changed/ran to test the hypothesis. Input used, before/after outputs.>
To test my hypothesis I did an assertion test for that function:
self.assertAlmostEqual(matching_characters("hello world", "hello world"), 11)
and it failed, saying matching_characters returned 10.

## Result
<Did the output confirm or contradict the hypothesis? New facts learned.>
It confirmed my hypothesis that it was skipping the last member of the string.

## Root cause
<The actual defect, stated as a mechanism (not just "line 42 is wrong").>
The defect was the wrongful len(expected) - 1 instead of a len(expected)

## Fix
<The change made, and the test(s) that now pass.>
I removed the - 1 and all tests passed.

## How I'd find it faster next time
<The technique/shortcut that would have narrowed this fastest.>
I'd say I found it really quickly, but I could have maybe checked the matching_characters function earlier but no I think I took all the right steps.