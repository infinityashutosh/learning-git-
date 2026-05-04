
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


