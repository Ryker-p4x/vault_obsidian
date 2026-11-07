Function arguments should usually be 0 whenever possible
Functions should have no more than 20 lines at maximum
Functions should only do one thing and do that thing incredibly

To tell if a function does one thing you can see if you can make another function out of it with a name that isn't just a restatement of its implementation, then it's a great function doing only one thing. This is apparently one of the hardest skills to master 

When to have monadic functions: 
- If you're asking a question about the argument, like boolean fileExists("file")
- If you're transforming the argument InputStream fileOpen("MyFile"). (Don't make these void like void includeSetupPageInto(StringBuffer pageText), so StringBuffer transform(StringBuffer in) is better than void transform-(StringBuffer out))
- When it is an event, example: void passwordAttemptFailedNTimes(int attempts) (the reader should have it very clear that this is an [[Event]])
When to have dyladic functions:
- On cartesian points like Point p = new Point(0,0) since new Point(0) would look weird
- You will eventually have to write some dyladic functions but they come at a cost and you should take advantage of what tools you have to try to make them all monadim functions.
When to have triad functions:
- Triad that makes more sense: assertEquals(1.0, amount, .001)

If you want to see more information on how to lower the argument count on a function go to: [[Techniques to lower argument count in a function]]

Never have functions with flag arguments.

Make sure the function doesn't do things that it shouldn't or aren't mentioned in the name that 
could damage something if the user isn't wary of it.

If your function must change the state of something, have it change the state of its owning object.

Functions that handle errors should do nothing else.

A function should either answer a question or do something, not both.
So if we had something like this:

``` cpp
if (set("username", "unclebob")) {
	// ...
}
// We could just make it into:
if (attributeExists("username")) {
	setAttribute("username", "unclebob");
	// ... 
}
```

