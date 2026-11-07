Very simple stuff so far in the introduction, I hate seeing visualizations, they're all so messy and hard to understand for me. Too overwhelming while small.
![[Pasted image 20261012135736.png]]
(genuine hell trying to read this)

Okay I tried to implement my own function and this was my initial version:

``` cpp
std::string remove_html_markup(const std::string &sentence) {
    std::string new_sentence = "";
    bool inside_markup = false;
    bool ignore_next_closing_sign = false;

    for (char c : sentence) {
        if (c == '<' && inside_markup == false) {
            inside_markup = true;
        } else if (c == '<' && inside_markup) {
            ignore_next_closing_sign = true;
        } else if (c == '>' && inside_markup &&
                   ignore_next_closing_sign == false) {
            inside_markup = false;
        } else if (inside_markup == false) {
            new_sentence.push_back(c);
        }
    }

    return new_sentence;
}
```

Mistakes: ignore_next_closing_sign is never reset
Two booleans for the same idea: How nested am I? Should've instead used a counter
Style == false instead of ! is wrong and sentence and new_sentence are weak names

In main, I use std::quoted which was wrong

Correct solution:
``` cpp
#include <iostream>
#include <string>
#include <string_view>

std::string remove_html_markup(std::string_view text) {
    std::string plain_text;
    plain_text.reserve(text.size());
    bool inside_tag = false;
    char open_quote = '\0';  // '\0' means we're not inside a quoted value

    for (char c : text) {
        if (!inside_tag) {
            if (c == '<') {
                inside_tag = true;
            } else {
                plain_text.push_back(c);
            }
        } else if (open_quote != '\0') {
            if (c == open_quote) {
                open_quote = '\0';
            }
        } else if (c == '"' || c == '\'') {
            open_quote = c;
        } else if (c == '>') {
            inside_tag = false;
        }
    }

    return plain_text;
}

int main() {
    std::string sentence;

    std::cout << "Enter sentence: \n";

    if (std::getline(std::cin, sentence)) {
        std::cout << remove_html_markup(sentence) << '\n';
    }
}
```

Okay so from what I've read, There's some devil solutions to these problems:

1. Obvious fix: Just add a if statement so that if it's a certain test then put in the correct solution (pretty dumb)
2. Using printf statements: If you forget to remove one single printf statement it can be catastrophic in some cases.

Things to do instead: You need to understand the code and then not fix the symptom, but the problem that's causing the symptom, then proceed systematically. (not sure what that means but okay)

The goal in debugging is to find the step in which the state of the program becomes faulty. 