
## multiple .gitignore
If a parent directory says "ignore all .txt files," but the child directory has a rule that says "don't ignore .txt files" (using the ! negation symbol), the child directory's rule wins for that specific folder.


"filename.txt" >> .gitignore 
to add a file to git ignore 


## ignoring in child directories 
1. Ignore by Name (Everywhere)

If you want to ignore a file named secret.txt no matter where it appears (root, child, or grandchild), simply type the filename:
    secret.txt

    Matches: secret.txt, folder/secret.txt, folder/subfolder/secret.txt.

2. The Double Asterisk ()

The  syntax is a powerful tool in Git that means "match any number of directories."

    To ignore a specific file in any subdirectory:
    **/config.json

    This ignores config.json in any child or grandchild folder, but not in the root directory.

    To ignore all files inside a specific folder name, regardless of where that folder is:
    **/temp_logs/
    This ignores any folder named temp_logs and everything inside it, whether it’s at root/temp_logs/ or root/child/grandchild/temp_logs/.

3. Deep Path Targeting

If you want to be more surgical and only ignore files in a specific branch of your folder tree, you can write out the path:

    child/grandchild/debug.log

    This will only ignore debug.log if it is exactly in that specific grandchild folder.




Branch deletion : 

git branch -d <branch name >







## Production reversal 

1. git log -n 5 --oneline
2. git revert <commit id>
3. I don't know what's the third step so just try it out anyways and figure it out


 how to revert changes in production , once the code is pushed

When code hits "production" and something goes wrong, the goal is to restore service as quickly as possible. In a professional environment, you have two main ways to handle this: Reverting (creating a new commit that undoes the changes) or Resetting (moving the branch pointer back).

Since you've already pushed the code to a remote server (like GitHub), git revert is almost always the safer choice.
1. The Safe Way: git revert

This is the "Forward-Fix" method. Instead of deleting history, Git calculates the exact opposite of your bad commit and creates a new commit to cancel it out.

Step 1: Find the Commit ID
Look at your history to find the "SHA" (the long string of numbers/letters) of the bad commit.
PowerShell

git log --oneline

Step 2: Revert it
PowerShell

git revert <commit-id>

    What happens: Windows might open a text editor (like Notepad or Vim) asking for a commit message. Just save and close it.

    The Result: Your folder now has a new commit that un-does the work.

Step 3: Push to Production
PowerShell

git push origin master

Why this is best: It keeps the history honest. Everyone else on the team will see exactly what happened and why the fix was made.
2. The "Undo" Way: git reset (Use with Caution)

If you are the only one working on the project and you want to "wipe away" the mistake as if it never existed, you can reset the branch.

Step 1: Move the branch back one step
PowerShell

git reset --hard HEAD~1

    --hard means "delete the changes from my files too." Warning: This erases unsaved work.

Step 2: Force Push
Because the remote server (GitHub) now has a "newer" version than your computer, it will reject a normal push. You have to force it:
PowerShell

git push origin master --force

Why this is risky: If anyone else pulled your "bad" code, their Git will break when they try to sync because you "rewrote history." In production, --force is usually disabled for safety.
3. Which one should you use?
Scenario	Recommended Command
Team Project / Production	git revert <commit-id>
Mistake was just made (Solo project)	git reset --hard HEAD~1
Only want to undo a specific file	git checkout HEAD~1 -- path/to/file.txt


so this line should be stashed and this won't come to the master branch if I switch now . 


git restore 
git reset hard/soft - undo commits till a specific point 
git revert - basically reverts the changes made in that specific commit 