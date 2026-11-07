# Why is the item count wrong by one extra? 

_Status: **finished** · created 2026-10-13 10:27 · updated 2026-10-13 10:56_ 
## Cycle 1 
### Hypothesis (step 2) purge_empty is incorrectly removing all empty items 
### Prediction (step 3) If the hypothesis is true, I should see how it fails to remove empty items in other tests. 
### Experiments (step 4) 
**Experiment 1** — 2026-10-13 10:40 Action: i added this 
``` python
def test_report_works_with_purge_empty(self):
	inventory = build_inventory() remove_stock(inventory, "item05", 5)   self.assertEqual(purge_empty(inventory), 39)
```
 to the test file - Evidence / result: ``` Traceback (most recent call last): File "/home/adrii/Work/scratch/debugging_practice/debuggingbook/debugging_exercises/test_exercise5.py", line 68, in test_report _works_with_purge_empty self.assertEqual(purge_empty(inventory), 39) ~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^ AssertionError: 1 != 39 ``` 


### Evaluation (step 5) 
 Outcome: **investigation finished** 
## Cycle 2 
### Hypothesis (step 2) 
There's an issue with purge_empty that makes it be wrong by one when there's more than 1 element being removed 
### Prediction (step 3) 
If it's true then I should see whenever I add more than one element it always failing by one 
### Experiments (step 4) **Experiment 1** — 2026-10-13 10:51 - Git: `not a git repository` - Action: 
``` python
def test_report_works_with_purge_empty(self): 
	inventory = build_inventory() 
	remove_stock(inventory, "item05", 5) 
	remove_stock(inventory, "item06", 5)                                             self.assertEqual(purge_empty(inventory), 2) 
	result = report(inventory)           
	self.assertEqual(result["item_count"], 39)
```
 
 - Evidence / result: ``` ====================================================================== FAIL: test_report_works_with_purge_empty (test_exercise5.TestInventory.test_report_works_with_purge_empty) ---------------------------------------------------------------------- Traceback (most recent call last): File "/home/adrii/Work/scratch/debugging_practice/debuggingbook/debugging_exercises/test_exercise5.py", line 69, in test_report _works_with_purge_empty self.assertEqual(purge_empty(inventory), 2) ~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^ AssertionError: 1 != 2 ``` **Experiment 2** — 2026-10-13 10:52 - Git: `not a git repository` - Action: 
 - def test_report_works_with_purge_empty(self): inventory = build_inventory() remove_stock(inventory, "item05", 5) remove_stock(inventory, "item06", 5) remove_stock(inventory, "item02", 5) remove_stock(inventory, "item01", 5) self.assertEqual(purge_empty(inventory), 2) result = report(inventory) self.assertEqual(result["item_count"], 39) - Evidence / result: ``` ====================================================================== FAIL: test_report_works_with_purge_empty (test_exercise5.TestInventory.test_report_works_with_purge_empty) ---------------------------------------------------------------------- Traceback (most recent call last): File "/home/adrii/Work/scratch/debugging_practice/debuggingbook/debugging_exercises/test_exercise5.py", line 71, in test_report _works_with_purge_empty self.assertEqual(purge_empty(inventory), 4) ~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^ AssertionError: 2 != 4 ---------------------------------------------------------------------- Ran 7 tests in 0.001s ``` 
 - ### Evaluation (step 5) Outcome: **investigation finished**

## Root cause
<The actual defect, stated as a mechanism (not just "line 42 is wrong").>
The defect was         if inventory[index]["qty"] == 0:
            inventory.pop(index)
            removed += 1
        else:
            index += 1
in this code there was no else statement and it was just index += 1 after, so whenever it'd get popped and all the elements would move to the left, it would move to the right again, skipping elements.

## Fix
<The change made, and the test(s) that now pass.>
I added an else statement so that if there wasn't a pop then it'd move right.

## How I'd find it faster next time
<The technique/shortcut that would have narrowed this fastest.>
Should've found out it was that function faster.