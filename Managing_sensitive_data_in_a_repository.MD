# Managing sensitive data in a repository

Commiting sensitive data, such as a password or SSH key into a Git repository is something that we must not do. This could put your entire application or bussiness in harms.

>Once you have pushed a commit to GitHub, you should consider any data it contains to be compromised. If you committed a password, change it! If you committed a key, generate a new one.

## How to manage sensitive data ?

The way to do is not to commit the file which contains sensitive data (password, username, ssh keys). What you should do is, keep your sensitive data in a config file such as `env.config` which is not tracked. Do not commit this file. Instead commit `env.config.example` which has sample data instead of real data.

You can put `env.config` in `.gitignore` to avoid committing.

## Removing sensitive data from the history

If you have already commited sensitive data, you need to remove it from the history as well. For that you can use either the git filter-branch command or the BFG Repo-Cleaner open source tool.

### BFG Repo-Cleaner:
This is an opensource tool which provides a faster, simpler ways of removing unwanted data. Link -> http://rtyley.github.io/bfg-repo-cleaner/

### Using `git filter-branch`
1. Clone the repository to your local computer if you don't have a copy.
2. Navigate into the repository and execute below command to,
   - Force Git to process, but not check out, the entire history of every branch and tag
   - Remove the specified file, as well as any empty commits generated as a result
   
   `git filter-branch --force --index-filter "git rm --cached --ignore-unmatch PATH-TO-YOUR-FILE-WITH-SENSITIVE-DATA" --prune-empty --tag-name-filter cat -- --all`
  You must run this command on all paths where there are files with sensitive data.
3. Add file to the `.gitignore` file.
4. Check the history to make sure you have removed the history and make sure all branches are checked out.
5. Force-push your local changes to overwrite your GitHub repository, as well as all the branches you've pushed up.
`git push origin --force --all`
6. Remove the sensitive file from your tagged releases.
`git push origin --force --tags`
7. Contact GitHub to remove cached views and references to the sensitive data in pull requests.
8. Collaborators must rebase, not merge, any branches they created off of your old (tainted) repository history.
9. Once you are confident that there are no side affects from this process, you can force all objects in your local repository to be dereferenced and garbage collected

## Reference
- http://help.github.com/en/articles/removing-sensitive-data-from-a-repository#purging-a-file-from-your-repositorys-history
- https://help.github.com/en/articles/removing-files-from-a-repositorys-history
- https://webcache.googleusercontent.com/search?q=cache:zBWxKeooTfoJ:https://snyk.io/blog/ten-git-hub-security-best-practices/+&cd=5&hl=en&ct=clnk&gl=sg
