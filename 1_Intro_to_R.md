## Get started with swirl ##

Swirl is a program run within R (or RStudio) that introduces you to R features and commands.

### Get set up for the tutorial ###
Request an RStudio session from Explorer, using the OOD interface. Tip: set the time to 2h instead of the default 1h.

Once you've connected to the RStudio server, work in the console window. 

Install swirl:
```
install.packages("swirl")
```
and load the library:
```
library(swirl)
```
Follow the prompts and select "R Programming" for the course. Work through the 15 lessons. Here are two ways to show your work for credit:

+ At the last prompt for each of the 15 lessons, screenshot the last line of output along with the message that tells you you're done and paste each one into a document. When all 15 last prompts/outputs are captured, save the document as a pdf and upload it to your assignment folder on Explorer.
+ Use the command `sink("<file_name>")` at the beginning of the RStudio session. All output will go to the file name you supplied. For the purposes of documenting that you completed swirl, you only need to show the output and not what you entered in the script window.
