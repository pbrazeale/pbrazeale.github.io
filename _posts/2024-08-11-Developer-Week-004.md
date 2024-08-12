## CS50X (Progress 64%)
### Week 5 Data Structures
#### Problem - Speller
"For this problem, you’ll implement a program that spell-checks a file, a la the below, using a hash table."


This kicked my ass! The lecture was excellent, but I struggled to wrap my head around pointers and hash tables.

Huge shoutout to Low Level Learning's [video](https://www.youtube.com/watch?v=2ybLD6_2gKM) on pointers; it made pointers click for me. I think it stemmed from the visual representation. 

Per Harvard's guidelines I can't share details on how I solved the problem itself, but I can discuss the knowledge gained and which secondary resources helped me the most. *If somehow you're reading this at the start of your programming journey, I highly recommend the [CS50X](https://cs50.harvard.edu/x/2024/) course.*

#### TODO
The speller problem proved too difficult for me to solve on my own; meaning I've uncovered my major knowledge weakness I need to address.

Toward that end, I've selected three courses to investigate further and complete at least one:
1. [The Last Algorithms Course You'll Need](https://frontendmasters.com/courses/algorithms/) by The Primeagen through Frontend Masters. Appears to be free.
2. [Data Structures and Algorithms Specialization](https://www.coursera.org/specializations/data-structures-algorithms) by UCSanDiego through Coursera.
3. [Data Structures & Algorithms](https://techdevguide.withgoogle.com/paths/data-structures-and-algorithms/) by Google via Google Tech Dev Guide.

I'm leaning toward the third option, though I suspect Primeagen's course would be more engaging. (*pure speculation*)

### Week 6 Python
Most of the assignments were just recreating what we had already done in C, using Python; which offers a deeper perspective to appreciate an abstracted language/OOP. Having already worked my way through half the Python course, made these assignment far easier.

I'm truly appreciative for the creation of Python. Using C was tedious.

Python documentation saved me so much time!
[Python CSV](https://docs.python.org/3/library/csv.html)

Total time to complete this week was quite low. I blew through the problem set until the DNA problem.

## [Specification](https://cs50.harvard.edu/x/2024/psets/6/dna/#specification)

- The program should require as its first command-line argument the name of a CSV file containing the STR counts for a list of individuals and should require as its second command-line argument the name of a text file containing the DNA sequence to identify.
    - If your program is executed with the incorrect number of command-line arguments, your program should print an error message of your choice (with `print`). If the correct number of arguments are provided, you may assume that the first argument is indeed the filename of a valid CSV file and that the second argument is the filename of a valid text file.
- Your program should open the CSV file and read its contents into memory.
    - You may assume that the first row of the CSV file will be the column names. The first column will be the word `name` and the remaining columns will be the STR sequences themselves.
- Your program should open the DNA sequence and read its contents into memory.
- For each of the STRs (from the first line of the CSV file), your program should compute the longest run of consecutive repeats of the STR in the DNA sequence to identify. Notice that we’ve defined a helper function for you, `longest_match`, which will do just that!
- If the STR counts match exactly with any of the individuals in the CSV file, your program should print out the name of the matching individual.
    - You may assume that the STR counts will not match more than one individual.
    - If the STR counts do not match exactly with any of the individuals in the CSV file, your program should print `No match`.


It took me over four hours to complete; most of which was reading the documentation and printing each variable to make sure I passed in the data correctly. Once I recalled how to access a dictionary, it went by easy.

Ran into one failed test, and was forced to refactor my code. Not sure it's the most elegant, but it does catch all known conditions. I'm pleased with it.

*This week's problem set made me excited to move back to CS50P. Thus far, Python is my favorite language.*


## Takeaways
I'm finally reaching the point where I have a rough idea of how to solve a problem when reading through the problem sets, before I prototype. My rough drafting is much faster, and I'm learning to compile frequently with print functions to make sure I'm manipulating the data correctly as I move.

I'm sure printing as I go is the slowest testing method, and I'll outgrow it soon, but for now I'm taking the W for understanding the blueprint in my head before implementation; instead of figuring it out as I go.

[Developer Week 003](https://pbrazeale.github.io/Developer-Week-003/)