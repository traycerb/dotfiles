# Dotfile How To (notes to myself):

The actual configuration file (e.g. _vimrc) is stored in this Dotfile directory.
A symlink to the file is created where the configuration file is needed (can't use hard links because git deletes the file when updating thus destroying the link, and can't use symlinks in the reverse direction because git copies the symlink itself, not the content it points to.  Creating a symlink as above guarantees when the file is deleted and subsequently updated, the symlink will still point to the same place, as the "new" file will still have the same name.

After making changes to the config file, save it.
Switch to a command prompt in the dotfiles directory
Add the modified file to the git staging area
```
  git add vim\_vimrc
```
Commit the file to the current branch
```
git commit 
```
...brings up vim editor to add commit message.  Write message and then press <esc> :wq
-or, add commit message on command line
```
git commit -m "My commit message"
```
You can combine the staging and commit and commit message like so:
```
git commit -a -m "My commit message"
```
You can push the current branch upstream (e.g. 'desktop') to a server (e.g. github or bitbucket, aliased as 'dotfiles' here, but commonly called 'origin')
```
git push dotfiles desktop
```
...depending on defaults, 'git push' alone is likely to work and push current branch up.
Alternatively after the commit, you can merge the changes into the master branch, before uploading
```
git checkout master
git merge desktop
git push dotfiles master
```
Switch back to the desktop branch if you want to leave the master branch in a stable state
```
git checkout desktop
```

The most straightforward git sequence would be:
```
git commit -a -m "My commit message"
git checkout master
git merge desktop
git push dotfiles master
git checkout desktop
```

This can be streamlined further with plugins (e.g. fugitive.vim), hooks, etc, but is useful for lite/learning purposes.

