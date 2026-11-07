If a function seems to need more than two or three arguments, try one of these.

Group arguments into an object

- If the same arguments always travel together, that's a missing class

cpp

```cpp
void drawLine(double x1, double y1, double x2, double y2, int thickness, Color color);
void drawLine(Point from, Point to, LineStyle style);
```

Make the arguments fields of a class

- If a few functions keep passing the same values around, make them member state and set them in the constructor
- Don't do this just to hide arguments, only if they're really part of the object's state

cpp

```cpp
double price(const Order& o, TaxTable t, Currency c);
double shipping(const Order& o, TaxTable t, Currency c);

class OrderPricer {
public:
    OrderPricer(TaxTable t, Currency c);
    double price(const Order& o) const;
    double shipping(const Order& o) const;
};
```

Split the function

- Lots of arguments usually means lots of jobs
- If an argument is only used in one branch, pull that branch out into its own function

cpp

```cpp
void saveUser(User u, bool sendEmail, EmailTemplate t, SmtpServer s);

void saveUser(User u);
void sendWelcomeEmail(User u, EmailTemplate t);
```

Get rid of flag arguments

- render(true) tells you nothing and proves the function does two things

cpp

```cpp
void render(bool isSuite);

void renderForSuite();
void renderForSingleTest();
```

Drop arguments you can calculate

- If one argument can be figured out from the others, don't ask for it

cpp

```cpp
double area(double width, double height, double ratio);
double area(double width, double height);
```

Use an options struct for optional settings

- C++ has no named arguments, so a struct with defaults works like one
- C++20 designated initializers make it read almost like named arguments


```cpp
void startServer(int port, int timeoutMs, bool useTls, int maxClients);

struct ServerOptions {
    int port = 8080;
    int timeoutMs = 3000;
    bool useTls = false;
    int maxClients = 100;
};

void startServer(ServerOptions opts);
startServer({.port = 9000, .useTls = true});
```

Use default values for the common case

- More than two or three defaults means you want an options struct instead


```cpp
void connect(const std::string& host, int port, int timeoutMs);
void connect(const std::string& host, int port = 443, int timeoutMs = 3000);
```

Use a list when the arguments are the same type

- average(a, b, c, d) is really one list argument

```cpp
double average(double a, double b, double c, double d);
double average(std::span<const double> values);
```

Inject dependencies in the constructor

- Things like a logger, database, or clock shouldn't be passed on every call, give them to the object once

```cpp
void saveOrder(Order o, Logger& log, Database& db, Clock& clock);

class OrderService {
public:
    OrderService(Logger& log, Database& db, Clock& clock);
    void saveOrder(Order o);
};
```

Pass behavior instead of switches

- When arguments only exist to steer the behavior, pass the behavior itself

```cpp
void sort(Items& items, bool byName, bool ascending);
void sort(Items& items, Comparator cmp);
```

- Return values instead of output arguments

- Same idea as the note about transform(StringBuffer in) being better than transform(StringBuffer out)

```cpp
void getBounds(int& x, int& y, int& w, int& h);
Rect getBounds();
```

Use strong types so arguments can't get mixed up

- This doesn't lower the count but it makes the arguments safer

```cpp
void transfer(int fromAccount, int toAccount, int amount);
void transfer(AccountId from, AccountId to, Money amount);
```

Use a context object carefully

- Passing one RequestContext beats passing six values through every layer
- Keep it small, or it turns into a global in disguise

```cpp
void handle(User u, Session s, Locale l, Config c, Logger& log);
void handle(RequestContext ctx);
```

Things to watch out for

- Don't make a meaningless Params class just to hit a number, five honest arguments are better than one vague object
- The same group of arguments showing up in many signatures is a sign you need a class (data clump)
- Callers passing nullptr, 0, or false just to skip arguments is a sign the function is doing too much
- Judge by how the call reads, not only by the count
