# Introduction
This project implements the Burrows-Wheeler Transform (BWT) and its associated algorithms for efficient string processing and pattern matching. The Burrows-Wheeler Transform is a fundamental technique widely used in bioinformatics, particularly in genome alignment tools, as well as in data compression algorithms.

The project builds a complete pipeline starting from a reference string and supports:

Construction of the suffix array
Generation of the Burrows-Wheeler Transform (BWT)
Computation of auxiliary data structures such as:
Count (first occurrence) table
Occurrence table
Implementation of backward search for fast exact pattern matching
Run-length encoding and decoding for compressing BWT output

# Pseudocode

```
1. BWT function:
- create an empty list
- loop through each index of the input string
    - create a rotation by: taking substirng from index i to end, then add substring from start to index i
    - add generated rotation to the list
- sort list in alphabetical order
- create an empty string for BWT result
- loop through each sorted rotation 
    - append the last character of the rotation to the BWI string
- return the BWI string

2. suffix_array
- create an empty list to store suffixes
- loop through the string by index 
    - create suffix starting from index i
    - append suffix and i as tuple to the suffixest list
- sort suffixes list
- create empty indexes list
- loop through sorted suffixes list
    - append each index to the indexes list
- return indexes list

3. BWT_from_suffix_array
- create an empty BWI string
- loop through each position in suffix list
    - if position = 0, then add last character of text to BWI string.
    - otherwise, add text[position -1] to BWI string
- return BWI string

4. cal_count
# Step 1: Count frequency of each character
    char_counts ← count occurrences of each character in string
# Step 2: Sort characters lexicographically
    sorted_chars ← sorted list of unique characters in string
# Step 3: Initialize output dictionary and cumulative counter
    smaller_counts ← empty dictionary
    cumulative ← 0
# Step 4: Compute number of smaller characters
    FOR each char IN sorted_chars:
        smaller_counts[char] ← cumulative
        cumulative ← cumulative + char_counts[char]
# Step 5: Return result    

5. cal_occur
- find and sort unique character from input bwt string
- create an empty occurency dictionary
- loop through each unique character, then create a list of zeroes with the same length as the bwt string
- loop through the bwt string:
    - identify the current character
    - if not the first posistion -> copy from the previou position for all characters
    - increase the count for the current character by one
- return the dictionary for occurence counts

6. update_range
- start with the current range defined by lower and upper
- for the given character a, compute the new lower boundary"
    - if lower boundary is 0:
        - set new lower to the starting position of the character a.
    - else: add the number of occurences of a before the lower boundary to the starting position of a. 
- compute the new upper bound:
    - add the number of occurence of a up to the upper boundary to the starting position of a
    - substract one to get the correct ending index
- return the updated lower and upper boundaries.

7. find_match
- add the end market to the reference string
- build the suffix array of the reference
- build the bwt string from the suffix array
- find count characters lexicographically smaller than each character
- find occurrences of each character up to each position
- set lower and upper as full range of reference
- read query from right to left
    - for each character, update the range using the count and occurence tables.
    - if the range become invalid, return an empty list. 
- after processing the whole query, use the suffix array position in the final range as match positions.
- sort the match positions and return them

8. run_length_encode
- if input string is empty, return an empty result
- set current character to the first character of the string
- set counter to 1
- create an empty string to store the encoded result
- scan through the string starting with second character to the end
- for each character:
    - if it's the same with the current chacteract -> increase counter by 1
    - otherwise:
        - add the current character and its count to the result
        - update current character to this new character
        - reset the counter to 1
- return encoded string

9. run_length_decode
- start with an empty decoded string
- set index = 0
- read one character
- read the digits that come after it to form the count
- convert the count to integer
- repeat the character that many times and add it to the decoded string
- return the decoded string
```

# Successes
Having a clear pseudocode foundation made the whole process feel much more manageable from the start. We had a set of steps to reference and work from, which set a solid foundation for the scripting. The pseudocode broke each function down into bite-sized pieces, so we could focus on one small part at a time. This was especially helpful for functions that had a lot of moving parts, and it also made it easier to write comments in our code, since we had descriptions of what each step was supposed to do. Overall, having that foundation in place gave the team confidence and a clear direction throughout the project.

# Struggles
Actually understanding what the algorithm was doing conceptually was a persistent challenge for us. Some of the core ideas were difficult to wrap our heads around, and translating a concept from a written description into working code required lots of prior planning. The biggest lesson was that understanding an algorithm well enough to explain it and understanding it well enough to implement it are two very different things. Additionally, with time constraints due to religious observances, our collaboration was strained. Regardless, we maintained communication to keep each other up to date, which ensured no one lagged behind.

# Personal Reflections
## Tien Nguyen
Working on this project was both challenging and rewarding, particularly in understanding the core concepts behind the Burrows-Wheeler Transform and backward search. I initially struggled with grasping how the count and occur tables work together to update the search range, and why the algorithm processes the query from right to left. It took multiple walkthroughs with examples for me to build a clear mental model of how these components map to matching positions in the original string. Despite these conceptual challenges, I found this project more manageable compared to others that required scaling to large, real-world datasets, since the focus here was more on understanding the logic and ensuring correctness rather than optimizing performance. Overall, this project helped deepen my understanding of advanced string algorithms and reinforced the importance of connecting theory with implementation.

## Fardina Tabassum
Other members' reflections on the project

## Shameem Shahib
I found the concepts to be very confusing at first, and it took some time to understand what was going on in each step. Nonetheless, it was a fun challenge to approach. We did have some obstacles due to time constraints and religious observations, but we made sure to update each other on what changes/updates were made. Working through each function helped me understand the concepts better, and I found that the hardest part was visualizing each step. Once that initial hurdle was crossed and we had our pseudocode laid out, the rest of the scripting was not as intimidating. Overall, I found this to be an enriching project that felt different from the previous projects we've worked on.

# Generative AI Appendix
As per the syllabus
