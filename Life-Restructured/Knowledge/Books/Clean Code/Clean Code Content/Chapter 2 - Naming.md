Why to use good names and not be lazy?
Good naming can make other programmers' lives easier and yours too while it may take longer it's an investment that'll be better in the long run. (it's relatively fine to use short names for functions that are small and aren't so important)

Class and Object names must be noun or phrase nouns with Class naming not having verbs
Functions should have the verb and then the noun in their naming.

Reuse words for concepts like adding, deleting, etc.

Avoid doing puns which is when you use the same name for things that do different things.
Avoid noise words (ProductInfo and Product are the same thing as a class)
Avoid encodings.
On interfaces and implementations it's better to name something NameImp than IName for Implementation Name.
WHen a constructor is overloaded make a static factory methods with names that describe the arguments
Complex fulcrumPoint = Complex.FromRealNumber(23.0); 
is generally better than
Complex fulcrumPoint = new Complex(23.0);

Don't use jokes or slang as definitions in code. Say what you mean and mean what you say.
