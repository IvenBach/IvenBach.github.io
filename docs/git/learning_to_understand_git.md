# Learning to understand git

Understanding version control and Git was not easy to learn for me. It took me longer than it should have. Thankfully I was fortunate to have several people willing to help and explain everything to me. The problem was me. I couldn't relate what I was told to anything I already understood. That made it relaly difficult to make progress. I understood the *words* that were used as part of the explanation but missed the underlying *meaning*. I was pointed towards [git documentation](https://git-scm.com/book/en/v2) and started reading. Again I read the words but missed the meaning. Despite lack of progress and frustration I continued on, this time searching out tutorials.

One that really helped had a [visual component](https://learngitbranching.js.org/). The breadcrumbing introduction it had along with seeing HEAD move as a commit occured made everything very understandable. After completing the tutorial I created a throwaway repository to test and further my understanding. It was at this point that a lot of what I read previously and read started to make sense.

## Initializing the throwaway-learning repo

I created a new directory, started Git Bash on that directory, then ran `git init` to [initialize](https://git-scm.com/docs/git-init) or start the repo.  
![Initializing the repo](Images/learning_to_understand_git/01_Initialized_the_repo.png "Create directories via Command Line Interface (CLI) with \`mkdir DirectoryName\`")

## Adding files

Next I added text files manually to the directory. I confirmed that these were seen with `git status` to [display the changes made](https://git-scm.com/docs/git-status).  
![Newly created files are seen](Images/learning_to_understand_git/02_Newly_created_files_are_seen.png "Creating empty files with \`touch FileName.txt\` or \`echo "File content" \> FileName.txt\`")

Then, as I did previously in the tutorials, I used the [add command](https://git-scm.com/docs/git-add) via `git add` to add the files to the index `git add First\ file.txt`.   
***\*\*\*Note - Autocompletion:*** If you type `git add Fir|` leaving the cursor blinking at `|` you can autocomplete the file name with Tab.  
***\*\*\*Note - Escape character:*** The `\` (backslash) is an escape character for the character that follows it, the ` ` &nbsp;(space) character. Files with spaces in their names need the spaces to either be escaped in this manner or otherwise enclosed in quotes `'` (single quote) or `"` (double quote). The following are also valid:

- `git add 'First file.txt'`
- `git add "First file.txt"`
 
![Adding the first file to the index](Images/learning_to_understand_git/03_Adding_the_first_file_to_the_index.png)

Adding files this way places them in the index, a preparation-area. It is a file of interest but isn't yet a part of the repo. Commonly called either staging-area or index, I use them interchangeably. The explicit `git add` step gives you the control to add only the files you want the repo.

Add the other files executing `git add .` where the `.` (period) indicates you want to add the new files. [Relevant StackOverflow question for adding files](https://stackoverflow.com/questions/572549/difference-between-git-add-a-and-git-add/16162511).  
![Add remaining files to the index](Images/learning_to_understand_git/04_Add_remaining_files_to_the_index.png)

## Committing to the repo

Now that the three files are in the staging area, add them to the repo via [git commit](https://git-scm.com/docs/git-commit). Execute `git commit -m "Initial commit"` where the `-m` is a flag/indicator that the following string `"Initial commit"` is the commit-message/descriptive-reason-it-was-added.  
![Initial files commited to the repo](Images/learning_to_understand_git/05_Initial_files_committed_to_the_repo.png)

## Detecting differences

??Ok now what? Time to see at what git can do for you. Delete one of the files. Execute `git status` and you'll see that it has been deleted. The file committed to the repository so from this point on it is tracked. Any differences in it, even a single character, will be brought to your attention as a change.  
![Deleted file identified by git](Images/learning_to_understand_git/06_Deleted_file_identified_by_git.png)

## Restoring from the repo
***Suggestion:*** Before continuing I suggest navigating to the directory you're working in to have it visible. Seeing the next command executed solidified the concept.

Because the file was committed to the repo you can restore it. Execute [git restore](https://git-scm.com/docs/git-restore) with `git restore Second\ file.txt` to bring the file from the repo back into the directory.

Now that I saw this in action I continued by creating two new files and editting those already existing.  
![New and edited files](Images/learning_to_understand_git/07_New_and_edited_files.png)

I restored one file with `git restore First\ file.txt`, and visually inspected it with a text editor confirming the changes weren't there. Executing `git status` confirmed no changes were detected. It was `restore`d back to the same state as when it was added to the repo.

Once again I made edits to First file.txt and saved them. Running `git status` confirmed they were there. ??What if I want to restore all the files? I executed `git restore .` followed by `git status` to see what changes were left. Naively I was a bit surprised to see files showing.  
![State after restoring all files](Images/learning_to_understand_git/08_State_after_restoring_all_files.png)

??Why are those files there? They shouldn't be there... Wait. Maybe they should be. :click: that's when another git puzzle piece connected; I understood the different areas of git. "Working Directory" is just that, the directory-where-work-is-done. Mentally changing the text on the middle arrow to "Stage changes=`git add`" helped.  
![The git areas image](https://git-scm.com/book/en/v2/images/areas.png)

Another image, git-lifecycle, from the documentation made sense as well.  
![Git lifecycle image](https://git-scm.com/book/en/v2/images/lifecycle.png)

When a new file is first seen it is untracked. I checked back up at the previous commands and the new files were indeed "Untracked files". After `git add` the files were in the Staged/Staging-Area, designated as "Changes to be committed".

My question now was ??how can I remove these files? I already knew I could delete them normally by right clicking and choosing delete, but this small taste of Command Line Interface (CLI) power had me hooked. I wanted more. I eventually found the command I wanted was [git clean](https://git-scm.com/docs/git-clean).

Since I wanted to remove both the remaining untracked files I executed `git clean .`. As before I watched the directory while I executed the command. Nothing happened. Confused, I then saw the output "fatal: clean.requireForce...".  
![](Images/learning_to_understand_git/09_Attempting_to_clean_untracked_files.png)

Reading the documentation `-i` was shorthand for `--interactive` "Show what would be done and clean files interactively". Going with that I executed `git clean -i .`  
![](Images/learning_to_understand_git/10_Cleaning_requires_aparameters.png)

The documentation for [interactive mode](https://git-scm.com/docs/git-clean#_interactive_mode) led me to executing option 1: clean.  
![](Images/learning_to_understand_git/11_Untracked_files_cleaned_away.png)

I forgot to watch the directory to see that they were removed but that didn't matter. At this point I knew I was on my way to learning to understand git.