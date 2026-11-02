# Introduction
Description of the project

# Pseudocode

def BWT()
```
IF "$" is not in String;
  APPEND $ TO String

word_matrix = EMPTY list

FOR char in String:
  SLICE last char and MOVE TO front
  UPDATE string TO new rotation
  APPEND new rotation to word_matrix

SORT word_matrix in lexicographic order

bwt = EMPTY string

FOR EACH rotation in word_matrix:
  bwt += rotation[-1]

RETURN bwt

```

def suffix_array()
```
IF "$" is not in String;
  APPEND $ TO String

word = EMPTY list

INITIALIZE starting position INDEX[i] TO 0

FOR char in String:
  SLICE from the starting position[i] To END
  APPEND suffix AND stating position to word 
  ADD 1 TO i until "$"

SORT word in Lexicographic order

lex_sort EMPTY list

FOR EACH suffix AND index in word:
  APPEND index TO lex_sort

RETURN lex_sort
```

def BWT_from_suffix_array()
```
new_string = EMPTY string

FOR EACH position IN input list:
  IF position == 0:
    GET LAST character of text
  ELSE:
    GET character before the position
  ADD character TO new_string

RETURN new_string
```

def cal_count()
```
CONVERT string TO list
SORT list in lexicographic order

count_dict = EMPTY dictionary

INITIALIZE starting position INDEX[i] TO 0

  FOR EACH char in sorted list:
  IF char is not already in count_dict:
    ADD char and its starting position i to count_dict

  ADD 1 TO i until all char in list have been processed

RETURN count_dict
```

def cal_occur()
```
CONVERT bwt_string TO list
SORT list in lexicographic order

occur_dict = EMPTY dictionary 

FOR EACH char in sorted list:
  IF char is not already in the dict
  INITIALIZE count TO 0
  occurrences = empty list

  FOR EACH character in original string
    IF character matches char:
    INCREASE count by 1

    APPEND count TO occurrences
  
  ADD char and occurences to occur_dict 

RETURN occur_dict
```
note for cal_occur: We noticed that the second example in the cal_occur() docstring has some incorrect occurrence counts. We followed the provided pseudocode and used inclusive running counts, which match the first example and correctly track how many times each character appears at every position.

def update_range()
```
Input: The current lower and upper boundaries, the count and occurrence dictionaries, and the character being processed.

Output: A tuple containing the updated lower and upper boundaries of the search range.

    IF character a is not in count OR occur:
        RETURN empty range (1, 0)

    IF lower is greater than upper:
        RETURN empty range (1, 0)

    GET the starting position of character a from count
    STORE this as character_start

    IF lower is 0:
        SET start_occurrences TO 0
        (no characters before the starting position)

    ELSE:
        GET the number of times character a appears
        BEFORE the lower boundary using occur[a][lower - 1]
        STORE this as start_occurrences

    GET the number of times character a appears
    UP TO AND INCLUDING the upper boundary
    STORE this as end_occurrences

    CALCULATE new_start by ADDING character_start,
    start_occurrences, and 1 for the $ row

    CALCULATE new_end by ADDING character_start
    and end_occurrences

    RETURN new_start and new_end as a tuple
```

def findmatch()
```

```


# Successes
Description of the team's learning points

# Struggles
Description of the stumbling blocks the team experienced

# Personal Reflections
## Group Leader
Group leader's reflection on the project

## Other member
Other members' reflections on the project

# Generative AI Appendix
As per the syllabus
