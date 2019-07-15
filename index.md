## Create python env with venv

Environments are usually located outside of the projects, like `~/environments`.
To create it:

```sh
cd ~/environments
python3 -m venv your-env
source ~/environments/your-env/bin/activate
```

After that, when you install dependencies, they will be installed in `~/environments/your-env`.

## Remove last commit, but keep changes

```sh
git reset --soft HEAD~1
```

Or `HEAD~2`, `HEAD~3`, etc. It will remove the last commit, but keep all changes staged (like you are about to commit).

## Move changes from one branch to another

You need to use [git cherry-pick](https://git-scm.com/docs/git-cherry-pick):

```sh
git cherry-pick 70ab296e22
```

You don't have to paste the whole hash, I think 8 chars are enough. So, the algorithm is the following:

1. Get a hash of commit you want to move to another branch (using `git log` or just from UI, like GitHub)
2. Checkout locally to the branch you want to use
3. Execute command `git cherry-pick ...`

You can paste a range, but I always pick one by one. There likely will be errors, so try to run your application and see how it works after each commit.

## Remove commit

If you want to remove the last commit, you can do

```sh
git reset --hard HEAD~1
```

This also works if you want to remove more than 1 commit, just change the number after `HEAD~`.

If you want to remove a commit in the middle, the easiest way to do so is via [git rebase](https://git-scm.com/docs/git-rebase):

1. Calculate how many commits ago is the one you want to remove
  - You can remove several of them, just count to the latest
2. Do an interactive rebase with N commits back: `git rebase -i HEAD~5`
3. It will open your editor, simply delete lines with commits you want to remove

## Better history in terminal

You can invoke a history in your terminal by pressing CTRL+r. Its interface is not the best, though, so you do improve it a lot by installing [https://github.com/junegunn/fzf].

After that, add this line to your `.zshrc` (not sure about regular bash):

```sh
[ -f ~/.fzf.zsh ] && source ~/.fzf.zsh
```

## Node/NPM

All executables are located in `node_modules/.bin`, like `node_modules/.bin/webpack`. You can execute it locally by one of those:

```sh
node node_modules/.bin/webpack
npx webpack # npm@5+
npm start # in package.json: "start": "webpack"
```

You can install packages locally by using relative path (absolute path will probably work too). Let's say that you have some library and your project on the same level. You can install it in your project by typing:

```sh
npm i ../library
```
