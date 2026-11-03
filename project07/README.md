# Introduction
This project has a purpose of guiding us on the process of understanding the Burrows-Wheeler Transform(BWT) algorithm and its applications in bioinformatics, specially when it is applied on  sequence alignment, pattern matching and data compression. We explored suffix array and the construction of BWT from the suffix array, which help to optimize data processing. Our group worked together to develop the pseudocode and translating it into Python, gaining a better understanding of the algorithm design, indexing and data structures associated with the algorithm. throughout this project, We improved our problem-solving skills, strengthened our collaboration as team and gained experience implementing the algorithm.

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
    IF query is empty:
        RETURN []
    ADD sentinel to reference

    BUILD suffix array
    BUILD BWT_from_suffix_array
    BUILD count table
    BUILD occurrence table

    lower ← 0
    upper ← LEN(BWT_from_suffix_array)

    FOR each character in query from right to left:

        lower, upper ← update_range()
        IF lower == upper:
            RETURN []

    # Step 6: Retrieve original positions
    matching_positions ← suffix_array[lower:upper]

    # Step 7: Return sorted positions
    RETURN SORT(matching_positions)
```
def run_length_encode()
```
    encoded_text ← ""

    IF LENGTH(input_text) == 0:
        RETURN encoded_text

    current_character ← input_text[0]
    count ← 1

    FOR i FROM 1 TO LENGTH(input_text) - 1:

        character ← input_text[i]
        IF character == current_character:
            count ← count + 1
        ELSE:
            encoded_text ← encoded_text + current_character + TO_STRING(count)
            current_character ← character
            count ← 1

    encoded_text ← encoded_text + current_character + TO_STRING(count)
    RETURN encoded_text
```

def run_length_decode()
```
    INITIALIZE string ← ""
    i ← 0

    WHILE i < LENGTH(encoded_text):

        character ← encoded_text[i]
        i ← i + 1
        count_string ← ""

        WHILE i < LENGTH(encoded_text) AND IS_DIGIT(encoded_text[i]):
            count_string ← count_string + encoded_text[i]
            i ← i + 1

        count ← TO_INTEGER(count_string)
        decoded_text ← decoded_text + (character REPEATED count TIMES)

    RETURN decoded_text
```

# Successes
One of our main successes was developing a better understanding of the Burrows Wheeler Transform algorithm and how the process of pattern matching can be accelerated by using Suffix Arrays. This project was a great opportunity to build on what we have been learning in class and apply our knowledge to a more complex algorithm.

# Struggles
I want point at what I think was the biggest challenge on this section which was the understanding and implementation of the upper and lower boundaries on the update_range function. At the end we worked together and we were able to resolve the problem and achieve the expected results.

# Personal Reflections
## Group Leader
Group leader's reflection on the project

## Member Graziano 
**Issues** I believe the biggest struggle was the understanding of the function update range. That is a big piece of the homework and it defines upper and lower bound. The calculation that will be the center of the encoding and decoding.

**What I Learn** While working on the project, we work as a team to resolve the pseudocode and understand to goal of the function and how each part was build. We for sure improved our reasoning skills and learn with algorithm.

**Next steps** I would like to keep building on this knowledge and how to use the Burrows-Wheeler Transform on different scenarios and problems. I also want to keep improving my ability to understand complex algorithms and its implementations.

# Generative AI Appendix
1. Description of which generative AI was used and its version.
Claude Opus 5

2. The entire prompt that was used to generate the content.
Can you help me to fix my pseudocode to a the github format? I need a better explanation of the Burrows-Wheeler Transform(BWT) algorithm and its applications in bioinformatics.

3. An explanation of how it was used (e.g., to generate ideas). I used it as a tool to learn the concepts described on the articles and materials, asking for further clarification on the material and extra examples.

4. A justification for why generative AI was used.

Sometimes just reading a concept and formula is not enough for me to have a grasp on the material, so I used it as an additional source to lean about the Burrows-Wheeler algorithm, and also to understand its optmization using suffix array.
