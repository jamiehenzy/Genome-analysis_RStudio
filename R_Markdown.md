```markdown
## Steps to Use R Markdown

1. **Create a new R Markdown file**
   - In RStudio, go to: File → New File → R Markdown...
   - A dialog box will pop up asking for title and author
   - Enter a title (like "Assignment 1") and your name
   - Click OK

2. **Save your file**
   - Go to File → Save (or use Cmd+S / Ctrl+S)
   - Give it a name like "Assignment1.Rmd"
   - Save it in your desired location

3. **You'll see a template document appear**
   - It has some example text and code chunks
   - You can delete everything BELOW the header (the part between the `---` lines at the top)
   - Keep the header! It should look like:
   ```
   ---
   title: "Assignment 1"
   author: "Your Name"
   date: "2025-10-02"
   output: html_document
   ---
   ```

4. **Add your question as regular text**
   - Below the header, type: `## Question 1: Perform a numeric calculation`

5. **Insert a code chunk**
   - Click the green "+C" button at the top of the editor (says "Insert a new code chunk")
   - OR type this manually:
   ````
   ```{r}
   
   ```
   ````

6. **Write your R code inside the code chunk**
   ````
   ```{r}
   5 + 10 + 23
   ```
   ````

7. **Test your code**
   - Click the green "play" arrow on the right side of the code chunk
   - You should see `[1] 38` appear below it

8. **Knit your document**
   - Click the "Knit" button at the top of the editor (it has a ball of yarn icon)
   - RStudio will create an HTML file showing both your code AND the output
   - The HTML file will automatically open in a viewer or browser
```
