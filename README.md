# Word clique

Find sequences of n-letter words where no words share letters. By default it
tries to find five 5-letter words with 25 distinct letters. This was
popularized by Matt Parker in [Can you find: five five-letter words with twenty-five unique letters?](https://www.youtube.com/watch?v=_-AfhLQfb6w).

## Description

The program takes one or more dictionary file names as arguments. The
dictionary files should contain one word per line. The program will then build
a list of candidate words by taking only words matching the target word length and containing only letters from `a` to `z` (case insensitive). Since the order
of letters in a word doesn't really matter for deciding if words share letters
it then converts each word to a canonical lower case anagram and removes any
duplicates. For each anagram it remembers the first corresponding word which it
will use for solution output (so the solutions will consist of dictionary words
instead of anagrams)

The distribution contains a number of sample dictionaries:

words.txt
: A big dictionary with many dubious words like `XDMCP`

words_alpha.txt
: Another big dictionary but already filtered so it only contains letters from `a` to `z` (in any case)

words_alpha_unique.txt
: The same as `words_alpha.txt` bit with anagrams removed

wordle-answers-alphabetical.txt
: Allowed answers in wordle. So it contains only 5-letter words

wordle-allowed-guesses.txt
: Allowed guesses in wordle. So it contains only 5-letter words

wordle.txt
: The combination of the worlde allowed answeres and allowed guesses. contains only 5-letter word

## Usage

Using `word-clique --help` will give an overview of how to use the program:

    Usage:
      word-clique [options] [<file>...]

    Options:
      --unique FILE         Write anagram unique words to FILE
      -l --length INT       Word length [Default: 5]
      -U --unbuffered       Line buffered (not default buffered)
      -T --no-tracker       No progress tracker
      --vowels              Only accept words with at least 1 vowel

      -h --help             Show this screen.
      --version             Show version.

`<file>` are the dictionary files to use. If not given it defaults to
`words.txt`.

For examle to generate the 538 solutions mentioned in [Can you find: five five-letter words with twenty-five unique letters?](https://www.youtube.com/watch?v=_-AfhLQfb6w) you can use:

    word-clique words_alpha.txt

To find four non-overlapping 6-letter words:

    word-clique -l 6 words_alpha.txt

Generating words from the combined wordle dictionary:

    word-clique wordle.txt

Sample output:

    8322 words with 5 letters, 5182 unique anagrams
    Load time: 0.0s
    26 letters: abcdefghijklmnopqrstuvwxyz
    Will search for 5 5-letter words with 25 unique letters
    Prepare: 2.5s
       78.3s: ['glent', 'prick', 'waqfs', 'vozhd', 'jumby']      1
       78.3s: ['glent', 'brick', 'waqfs', 'vozhd', 'jumpy']      2
       89.7s: ['treck', 'pling', 'waqfs', 'vozhd', 'jumby']      3
       89.7s: ['treck', 'bling', 'waqfs', 'vozhd', 'jumpy']      4
       99.4s: ['kreng', 'clipt', 'waqfs', 'vozhd', 'jumby']      5
      117.3s: ['kempt', 'waqfs', 'brung', 'cylix', 'vozhd']      6
      117.9s: ['cimex', 'waqfs', 'blunk', 'grypt', 'vozhd']      7
      118.1s: ['gucks', 'waltz', 'vibex', 'fjord', 'nymph']      8
      118.6s: ['bemix', 'clunk', 'waqfs', 'grypt', 'vozhd']      9
      118.6s: ['gymps', 'waltz', 'vibex', 'chunk', 'fjord']     10
    Finish: 118.9s, 10 solutions
