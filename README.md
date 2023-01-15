# ai-music-composer
Ann AI music composer. It should be able to learn some statistics from a number of given strings representing famous musical pieces and then use these statistics to generate new strings representing new pieces.

Using this website http://virtualpiano.net/. It provides a virtual piano on which you can play using the keyboard. Moreover, it provides music sheets of a collection of famous songs.

For this project, we have chosen a number of strings from those provided on the virtual piano website and modified them a bit so that they would include only the characters [0-9], [a-z] and [’B’,’C’,’D’,’E’,
’G’,’H’,’I’,’J’,’L’,’O’,’P’,’Q’,’S’,’T’,’V’,’W’,’Y’,’Z’]. The file MusicResources.hs will con- tain these strings. Your code should use the list training from that file in order to learn. Make sure you have that file in the same folder as your solution .hs file. Then, you can write in your file:
import MusicResources

In order to implement the composer, you are required to:

a) Implement the function makeStatsList which will dynamically generate a list of statistics accor- ding to the content of the training list in the MusicResources.hs file. The type of makeStatsList will be:
     makeStatsList :: [(Char,[(Int,Char)])]
The size of the output list will be 54 items since we have 54 different characters to gather statistics about. Every entry in that list is a pair representing statistical information about a specific character which is the first item of the pair. The second item in the pair is a list of pairs containing which other characters appeared directly after that specific character and with what frequency. Each inner list has to be sorted from the highest to the lowest frequency value.

b) Implement the function compose:
     compose :: Char -> Int -> [Char]
The input to this function will be a character representing the start of the musical piece and an integer representing the total length of the musical piece that should be generated. The compose function has to call makeStatsList to use the information gathered in the composition process as follows: For every character in the output string, the next character will be determined as a random variable that can take values from the set of next possible characters according to our statistics. However, when the value of the next character is being randomly chosen, the weights of the frequency of each option have to be taken into consideration. For example, assume the currently character is ’0’ and the statistics pair of ’0’ is:
     (’0’,[(8,’w’),(2,’q’)])

Then, the next character chosen should be ’w’ with a probability of 80% and ’q’ with a probability of 20%. This is because the only two possible next characters in the training strings are ’w’ and ’q’ with frequency 8 and 2, respectively. Hint: You can use the function randomZeroToX in your solution which you will find in MusicResources.hs.


### Sample Test
a) The file makeStatsListCall.txt shows the output of a sample makeStatsListCall that was generated with a value of the training list equal to:
     training =  [furElise, moonLightSonata,secondWaltz, preludeInCMajor, caspersLullaby]
b) The fun part of this project is that you can open the virtual piano website and play the strings your code outputs in part b of the project. We are providing you with a script file that will help automate the process of sending keystrokes corresponding to the musical piece string to Mozilla Firefox.
Example:
     Main> compose ’e’ 25
     "euoyuoetusauotyuodgdadgti"
