# Programming Fundamentals And Web

## Python

### Comments

- Use `#`
- `# NOQA` for no quality assurance of code

### Classes

```
import media

toy_story = media.Movie("Toy Story", "Toys come to live", "link.jpg", "link")
# new instance of movie, __init__ gets called, toy_story = self

print(toy_story.storyline) # prints storyline
toy_story.show_trailer # opens browser and plays trailer
print(media.Movie.VALID_RATINGS) # returns list of valid ratings stored in class Movie()
media.Movie.__doc__ # returns first string in class Movie()
```

```
import webbrowser

class Movie():
  """ Some text to describe class"""

VALID_RATINGS = ["G", "PG", "PG-13", "R"]

def __init__(self, movie_title, movie_storyline, poster_image, trailer_youtube):
  self.title =  movie_title
  self.storyline = movie_storyline
  self.poster_image_url = poster_image
  self.trailer_youtube_url = trailer_youtube

def show_trailer(self):
  webbrowser.open(self.trailer_youtube_url)
```

- Write class name with capital letter
  - [Google Styleguide](https://google.github.io/styleguide/pyguide.html)
- `self` is not keyword but convention, can be replace by any other name in all occurances
- Class vocabulary: class, constructor, instance variables, instance methods, instances
  - [Screenshot](https://postimg.org/image/4334faz6v/)

#### Class Inheritance

```
class Parent():
  def __init__(self, last_name, eye_color):
    print("Parent Constructor Called")
    self.last_name = last_name
    self.eye_color = eye_color

  def show_info(self):
    print("Last Name - " + self.last_name)
    print("Eye Color - " + self.eye_color)

class Child(Parent): # show inheritance from class Parent()
  def __init__(self, last_name, eye_color, number_of_toys):
    print("Child Constructor Called")
    Parent.__init__(self, last_name, eye_color)
    self.number_of_toys = number_of_toys

  def show_info(self)
    print("Last Name - " + self.last_name)
    print("Eye Color - " + self.eye_color)
    print("Number of toys - " + str(self.number_of_toys))

billy_cyrus = Parent("Cyrus", "blue")
print(billy_cyrus.last_name)
billy_cyrus.show_info()

miley_cyrus = Child("Cyrus", "blue", 5)
miley_cyrus.show_info()
```

- Method overriding

## HTML & CSS Basics

### Structure

```
<!DOCTYPE html>

<html>
<head>
<title>Quiz - Hello, world!</title>
    <style>
    p {
    color: blue;
    }
    /- add CSS here -/
    </style>
</head>
<body>
<h1>Hello, world!</h1>
<p>Are you ready for your first challenge?</p>
<p>Let's add some style to this webpage!</p>
</body>
</html>
```

### Comments

- HTML
  - `<!-- This is comment -->`
- CSS
  - `/- add CSS here -/`

### IDs

- Can only be applied to one element
- One element can only have one ID
- Use classes otherwise
- Refer to in CSS by `#id-name {}`

### Classes

- Can be added to multiple elements
- Elements can have multiple classes, separate by spaces, order of classes does not matter
- Refer to in CSS by `.class-name {}`

### Browser Developer Tools

- Open by <kbd>CMD</kbd> + <kbd>Alt</kbd> + <kbd>I</kbd>
- Use console to find specific class or ID
  - Type `$('[selector]')` where `[selector]` is certain .class or #id

### Colors

- Chrome has built in color picker tool, developer tools and click on specific color icon to open, also includes color picker

#### RGB

- Amount of red, green, blue written as decimal number between 0-255
- background-color: rgb(255, 0, 255);

#### Hexadecimal

- Amount of red, green, blue written as hexadecimal number between 00-FF
- FF corresponds to 255
- background-color: #ff00ff;
- Short hexadecimal #00f corresponds to #0000ff

### Shadow

- [CSS Matic Box Shawdow](http://www.cssmatic.com/box-shadow)

### Fonts

- Web safe fonts
  - [CSS Font Stack](https://www.cssfontstack.com)

### Stylesheet

- File containing all CSS for website
- Insert in `<head>`
  - `<link href="path-to-stylesheet/stylesheet.css" rel="stylesheet">`

```
<head>
  <title>My Webpage</title>
  <!-- ... -->
  <link href="path-to-stylesheet/stylesheet.css" rel="stylesheet">
  <!-- ... -->
</head>
```

### Sizing

- Box model
  - Every element has
    - Content,
    - Padding,
    - Border,\
    - Margin
  - Box sizing
    - content-box: width and height do not include padding, border and margin, only content
    - border-box: width and height include content, padding and border but not margin (normally assumed)
- Block elements
  - Take as much width as possible, constraint-based
  - Take as much height as needed, as short as possible, content-based
- Inline elements
  - Only as wide as needed
  - Similar to block elements but content based meaning only as wide as content inside meaning only as wide as content inside
  - Cannot set width and height of inline elements
  - Can accept margin and padding, margin will not push vertically
- Inline-block elements
  - Can be sized like block elements but are laid out like inline elements
- Percentages always calculated in relationship to immediate parents
- Sementic elements
  - Help to structure site
  - Improves for search engine crawlers, helps SEO
  - Div soup: when only divs are used inside each other

### Semantic Elements

- `<article>`,`<aside>`, `<footer>`, `<header>`, `<main>`, `<nav>`, `<section>`
- Can contain other elements
- Explain content of web page

## Positioning

- Document refers to DOM (Document Object Model), entire page
- Window or viewport is visible portion of DOM in browser window

### Static Position

- Normal position, default
- Block elements
  - Aligned vertically meaning left outer edges line up
- Inline elements
  - Aligned horizontally and if inline element is too big for line, it wraps around next line
- Inline-block
  - Hybrid element
  - Can have defined width and heigt but can still appear in same line as other elements
  - `display: inline-block` elements take on layout behaviour of inline element with sizing behaviour of block element
- Span elements are inline, div elements are block and take their own line

### Anonymous Boxes

```
.child {
  display: inline-block;
  width: 50%;
}
```

This renders differently:

```
<div class="container">
  <div class="child">Child 1</div>
  <div class="child">Child 2</div>
</div>
```

Than this:

```
<div class="container">
  <div class="child">Child 1</div><div class="child">Child 2</div>
</div>
```

Due to whitespace, newline and tab between elements

### Relative Position

- Behaves like normal flow
- Allows to shift position of element after they have been laid out in normal flow
- Properties top, left, bottom and right are adjustments to normal flow
- Use only top or bottom and left or right at time

### Fixed Position

- top, bottom, left and right indicate position within viewport
- Elements do not move as user scrolls

### Absolute Position

- Element is positioned relative to its parent before rest of normal flow occurs
- Siblings in normal flow ignore absolute positioned element
- Rarely best positioning option

### Tabular Overview

| | Relative | Absolute | Fixed
|-|-|-|-|
| _When_ | After normal flow | Before normal flow | Before normal flow|
| _Positioned relative to_ | Position in normal flow | Parent | Viewport |

### Third Dimension

- Z-axis controlled by `z-index` property

### Floats

- Own property `float`
  - `float: left`
  - `float: right`
- Normal flow line boxes respect boundaries of floated elements, but normal flow block elements ignore floats
- Float children are not involved inbox-size calculation of normal flow parents

## Responsive Design

### Emulators

- [BrowserStack](https://www.browserstack.com) to test multiple web browsers
-  Alternatively Chrome browser development tools
  - Click phone icon
  - Choose device, resolution,  and browser
- Use Chrome Canary optional
  - Developer version of Chrome
  - Includes new and experimental features but not guaranteed to be stable

### Pixels

- Device Independent Pixels (DIP) as physical unit of measurement based on coordinate system, abstraction of pixel that can be converted to physical pixel
- Hardware pixels
- Device pixel ration
  - Hardware pixel divided by (DIP)
- Example: iPad has DIP of 1024x1366 but hardware pixels lead to resolution of 2048x2732
- `min-width` refers to width of window
- `min-device-width` refers to width of total screen

### Viewport

- `<meta name="viewport" content="width=device-width,initial-scale=1">`
	- Insert in head to control viewport's size and scale

### Media Query

Allows to use multiple CSS sheets based on screen resolution

```
<link rel="stylesheet" href="styles.css">
<link rel="stylesheet" media="screen and (min-width: 500px)" href="over500.css">
```

Adjust certain classes based on screen resolution

```
body {
  background-color: green;
}

@media screen and (max-width: 400px) {
  body {background-color: #F79420; }
}

@media screen and (min-width: 600px) and (max-width: 800px) {
  body {background-color: green; }
}

@media screen and (min-width: 801px) {
  body {background-color: blue; }
}
```

### Flexbox

- Layout mode that allows to arrange items within container
- Easy to position child elements
- Container's margin does not collapse with margin of its content
- Order of elements can easily be changed
- Set for container parent element:
	- `display: flex;`
	- `flex-direction: row` or `flex-direction: column`
	- `flex-wrap: wrap`, `flex-wrap: nowrap` or `flex-wrap: wrapreverse`
	- `align-items: flex-start` to reduce child element height to minimum aligned on top, alternatively `align-items: flex-end` to align at end, `align-items: flex-center`, default is `align-items: stretch`
	- `justify-content: space-between;` to spread content
- Set for child element:
	- `flex: 2;` for relative width
	- `order: 3;` for order in grid
- Adding `flex-wrap: wrap;` allows elemetns to wrap to next line

```
.container {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
}
```

- Flexbox example with multiple sizes and order

```
header {width: 100%; order: 1; }
.red {width: 50%; order: 2; }
.orange {width: 50%; order: 3; }
footer {width: 100%; order: 4; }
.light_blue {width: 20%; order: 5; }
.dark_blue {width: 60%; order: 6; }
.green {width: 20%; order: 7; }
```

## Resources

- [Mozilla Developer CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [CSS Tricks Almanac Reference Guide](https://css-tricks.com/almanac/)
  - Also good for design inspiration
- [D3 Gallery Graphics and Charts](https://github.com/d3/d3/wiki/Gallery)
  - Create graphics and charts on web
- [PEP8 Online Checker](http://pep8online.com)
- [A List Apart](http://alistapart.com)
  - Design, development and meaning of web content
  - Article and news
- [Flexbox](http://flexboxgrid.com)
- Flexbox Tutorial: [Flexbox CSS in 20 Minutes](https://www.youtube.com/watch?v=JJSoEo8JSnc)
- Flexbox Tutorial: [Flexbox Tutorial Real Layout Examples](https://www.youtube.com/watch?v=k32voqQhODc)
- Device Pixel Metrics: [Material.io](https://material.io/devices/)
- Validator
	- [CSS Validator](https://jigsaw.w3.org/css-validator)
	- [HTML Validator](https://validator.w3.org/)

# Developer Tools

## Shell

- Programming language
- Shell scripts

### Open Terminal

- On Windows
  - Install Git Bash from [Git-SCM](https://git-scm.com/download/win) and run it
- On Mac
  - Run terminal

### Commands

- `echo Hello World`
  - Print statement
- `open index.html`
  - Open index.html file
- `ls`
  - Lists current directory
- `ls Downloads`
  - Lists Downloads directory
- `ls ~`
  - Lists home directory
- `ls -l Downloads`
  - Returns more detailed list of directory
- `ls -l Downloads/*.pdf`
  - Returns all PDFs in directory
- `pwd`
  - Print working directory
- `cd ..`
  - Change directory to previous
- `mkdir Documents/Books`
  - Create new folder in Documents directory
- `mv 'Documents/Bookname.epub' Documents/Books/`
  - Moves file to new folder
- `curl http://google.com`
  - See URL
  - Returns URL content
- `curl -L http://google.com`
  - Returns also redirects
- `curl -o filename.html -L http://google.com`
  - Downloads full HTMl of website as file
- `cat dictionary.txt`
  - Can read any file
  - Short for concatenate
- `less dictionary.txt`
  - Returns one screen of file at time
  - Use enter, space and arrow keys to continue
  - Press b to go back
  - Use / to search
  - Press q to quit
- `rm Dictionary.txt`
  - Remove file
  - File will be delete immediately
- `rm -i Dictionary.txt`
  - Will show prompt before removing
- `rmdir Books`
  - Removes directory
- `rm *'Bad'*`
  - Removes all files containing 'bad'
- `grep someword dictonary.txt`
  - Reads file and returns all lines containing 'someword'
- `grep someword dictonary.txt | less`
  - Sends output of grep in less command
  - Grep for someword in dictionary.txt and pipe it to less
- `curl -L http://google.com | grep someword`
  - Output of curl command gets fed into grep command
- `curl -L http://google.com | grep someword | wc -l`
  - Adding word count for lines
  - Returns number of occurences of someword in URL
- `curl -L http://google.com | grep -c someword`
  - Alternative way for returning word count
- `cat requirements.txt`
	- Check content of file
- `clear`
  - Clears shell
- `-l` or `-i` are called flags used to used to alter functions e.g. displaying long information

### Variables

#### Shell Variable

- Internal to shell program itself
- `variablename='one two three'``
  - Setting variable
- `echo $variablename`
- `$LINES`
  - Predefined
- `$COLUMNS`
  - Predefined

#### Environment Variables

- Shared with programs that are run inside shell
- `$PWD`
- `$LOGNAME`
  - Returns username
- `$PATH`
  - Returns paths where shell is looking for programs to run
  - When program is started, its directory needs to be included in $PATH variable
- `PATH=$PATH:/newdirectory/here`
  - Change will only last until shell is closed

### Customizing Shell

- Edit .bash_profile file
  - .bash_profile file will be run every time shell starts
  - File can also include variable assignments
  - Add program directory to shell configuration file to keep it in paths
  - Special case for Linux, look up .bashrc file
  - `ls -a`to find file
  - `atom .bash_profile` to open
- `PS1='$ '`
  - Edit $PS1 shell variable to change initial shell prompt
  - $PS1 can also be added to .bash_profile file to remain
  - [PS1 Generator](http://bashrcgenerator.com)

### Alias

- `alias ll='ls -la'`
  - Give short name to longer command
  - Type short short command for shell to run long command
- `alias cl='curl -L'`
- `alias ..='cd ..'`
- `alias now='date +"%T"'`
- `alias`
  - Returns all aliases
- Alias lasts only if shell is closed
- For alias to remain, store it in .bash_profile file

### Additional

- Multiple commands can be separated by ;
- Put URLs in quotes if contain special characters like & which have unusual meanings to shell

## Version Control

- Most popular version control systems: Git, Subversion, Mercurial
- Centralized versus distributed version control (Git)
- Source Code Manager (SCM)
- Download [Git-SCM](https://git-scm.com/downloads)
- Run `git` on command line

### Configuration On Mac

```
<!--- sets up Git with your name --->
git config --global user.name "<Your-Full-Name>"

<!--- sets up Git with your email --->
git config --global user.email "<your-email-address>"

<!--- makes sure that Git output is colored --->
git config --global color.ui auto

<!--- displays original state in conflict --->
git config --global merge.conflictstyle diff3

git config --list

<!--- set up Atom as text editor --->
git config --global core.editor "atom --wait"
```

### Commands To Create And Review

- `get init`
	- Go to directory first
	- Create new repository
- `get clone`
	- Copy existing repository to local computer
	- Pass path or URL to command
	- Repositories can not be nested, current working directory should not be in Git repository
	- `git clone https://github.com/udacity/course-git-blog-project` to clone form URL
	- `git clone https://github.com/udacity/course-git-blog-project blog-project` to clone from URL and rename
	- Command does not change shell directory, not to go inside new repository
- `git status`
	- Check status of repository
	- Use frequently, always first thing to check
- `git log`
	- Display information about existing commits and changes made
	- By default command displays
		- SHA which is unique for every commit
		- Author
		- Date
		- Message
- `git log --oneline`
	- Only displays short SHA and message
	- One line per line
- `git log --stat`
	- Displays files that have been modified in commit and number of lines that have been added or deleted
- `git log -p`
	- Displays actual changes made to files
	- `-p` is short for `--patch`
	- Lines with plus symbol have been added in commit
	- Index shows hash of original file and of new file
	- `@@ -[starting line in original], [number of lines in original] +[starting line in new], [number of lines in new] @@`
		- Shows where changes have been made
- `git log -p --stat`
	- Displays both stats info above patch info
- `git log -p fdf5493`
	- Will display all commits up to provided SHA
- `git show`
	- Displays information about given most recent commit
	- Can be combined with `--stat` or `-p`
- `git show fdf5493`
	- Displays information about commit of provided SHA
- `rm -rf .git`
	- Removes all Git repository files from current directory

```
$ git log
commit 6f0b3684ed2c549bc9cbb2c504c8ccc567407e79 (HEAD -> master)
Author: Kai <mail@example.com>
Date:   Sat Oct 7 19:54:54 2017 +0200

    Add header to body

commit 7abbac20cfdbcea3c61c1563af8ec1900eafe307
Author: Kai <mail@example.com>
Date:   Sat Oct 7 19:46:08 2017 +0200

    My first commit
```

#### Scroll In Commit

- Scroll down
	- <kbd>j</kbd> or <kbd>↓</kbd> to move down one line at time
	- <kbd>d</kbd> to move by half page screen
	- <kbd>f</kbd> to move by whole page screen
- Scroll up
	- <kbd>k</kbd> or <kbd>↑</kbd> to move up one line at time
	- <kbd>u</kbd> to move by half page screen
	- <kbd>b</kbd> to move by whole page screen
- <kbd>q</kbd> to quit out of log

### Commands To Add Commits

- `git add`
	- Add files from working directory to staging index
	- Initially: create index.html, CSS and JS file in directory and check status
	- For Git to track files, they need to be in repository folder
	- To commit file, it needs to be in staging index
- `git add index.html`
	- Adds index.html to staging index
- `git add index.html css/app.css js/app.js`
	- Adds three files to staging index
	- Space separate file names
- `git add .`
	- Adds all files to staging index
- `git rm --cached index.html`
	- Removes file from staging index
	- File will be unstaged
- `git commit`
	- Take files from staging index and take them to repository
	- Opens code editor
	- Type commit message on first line of editor
	- Lines starting with # are comments and are not recorded
	- Save and close tab and window in editor
	- Terminal should display commit message and commited files
- `git commit -m "Some commit message"`
	- Shortcut to avoid opening code editor
	- Allows short commit message
- `git commit -a -m --allow-empty-message`
	- Allows to commit without message
	- `-a` will stage changes adjusted for modified and deleted files
- `git diff`
	- Displays changes that have been made but have not been commited yet

```
$ git commit
[master (root-commit) 7abbac2] My first commit
 3 files changed, 14 insertions(+)
 create mode 100644 css/app.css
 create mode 100644 index.html
 create mode 100644 js/app.js
```

```
$ git diff
diff --git a/index.html b/index.html
index cfaf56f..641eca2 100644
--- a/index.html
+++ b/index.html
@@ -10,9 +10,9 @@
 <body>

   <header>
-      <h1>Expedition</h1>
+      <h1>Adventure</h1>
   </header>
-
+
     <script src="js/app.js"></script>
 </body>
 </html>
 ```

- Avoid files inside project directory from being committed
  - Create file with name ".gitignore" in same directory as .git is located
  - File used to tell Git about files not to track
  - List names of files that should be ignored in file
  - Use globbing to add multiple files e.g. images
    - Use special charactes to match patterns
    - `#` marks line as comment
    - `*` matches 0 or more characters
    - `?` matches 1 character
    - `[abc]` matches a, b, or c
    - `**` matches nested directories, `a/**/z` matches a/z, a/b/z, a/b/c/z
    - Enter `samples/*.jpg` in file to match all images in folder "samples"

```
$ git status
On branch master
Changes not staged for commit:
	modified:   index.html

Untracked files:
	.gitignore

no changes added to commit
```

#### Good Commit

- Each commit should have single focus
- Changes should be related
- Short commit message with about 60 characters
- Message should explain what was changed but not why and how
- Do not use word "and", instead split up in multiple commits

### Tags

- `git tag`
	- Displays all tags in repository
- `git tag -a v1.0`
	- Adds tag "v1.0" to last commit
	- Make commit stand out from others
	- Tag stays logged to commit
	- `-a` will create annotated flag otherwise lightweight tag is created
		- Annotated tags includes additional information about author, date and message
	- Command will open code editors
	- Enter tag message at top
	- Save and close tab and window in editor
- `git tag -a v1.0 a87984`
	- Adds tag "v1.0" to commit a87984
	- Any commit in repository can be tagged
- `git tag -d v1.0`
	- Deletes tag "v1.0"

### Branching

- Branching allows multiple lines of development to develop multiple features in parallel
- `git branch`
	- Command returns list of all branch names in repository and shows active branch
	- Default name of first branch is "master"
	- Head is pointer to active branch
- `git branch sidebar`
	- Creates branch "sidebar"
- `git branch alt-sidebar-loc 42a69f`
	- Creates new branch "alt-sidebar-loc" and has it pointing at commit with SHA 42a69f
- `git branch -d sidebar`
	- Once change on secondary branch is completed, it can be combined with "master" branch
	- Deletes "sidebar" branch
	- Currently active branch can not be deleted, switch branches first
	- Branch can not be deleted either if it has commits that are not on any other branch
- `git branch -D sidebar`
	- Forces to delete "sidebar" branch
- `git checkout sidebar`
	- Switch to "sidebar" branch
	- Switch between different branches and tags
	- Used to switch branch to which head is pointing to
	- Checkout will remove files that are referenced by commits in previous branch, will replace them with files that are referenced by commits in "sidebar" branch
- `git checkout sidebar`
	- Switch to "master" branch
- `git checkout -b another-sidebar master`
	- Creates new branch "another-sidebar" starting at same location as master branch and directly switches to new branch
- `git log --oneline --graph --all`
	- `--graph`adds bullets and lines to leftmost par of output showing actual branching
	- `--all` displays all branches in repository

```
$ git log
commit b6fca9bc5ed43e06a2d6593f8899b893587ea0ba (HEAD -> master, tag: v1.0)
Author: Kai <mail@example.com>
Date:   Sat Oct 7 20:16:12 2017 +0200

    Change heading

commit 6f0b3684ed2c549bc9cbb2c504c8ccc567407e79
Author: Kai <mail@example.com>
Date:   Sat Oct 7 19:54:54 2017 +0200

    Add header to body
```

```
$ git branch
  master
* sidebar
```

```
$ git log --oneline
b6fca9b (HEAD -> sidebar, tag: v1.0, master) Change heading
6f0b368 Add header to body
7abbac2 My first commit
```

```
$ git log --oneline --graph --all
* 29820fe (HEAD -> footer) Add links to social media
* ba64460 (master) Heading changed again
* 143341e Add body color
| * b570f06 (sb) Added custom text
| * b452e16 Aside added
|/
* b6fca9b (tag: v1.0) Change heading
* 6f0b368 Add header to body
* 7abbac2 My first commit
```

### Merging

- Combines changes made on different branches
- Merge happens towards head pointer meaning other branch will be merged into currently checked-out branch
- `git merge sidebar`
	- Merges "sidebar" into "master"
	- "Master" is currently checked-out branch
- When merge happens
	- Git looks back along history
	- Finds single commit that both branches have in history
	- Combines lines of code that were changed on separate branches together
	- Makes commit to record merge
- Fast-forward merge
	- Will move currently checked-out branch forward until it points to same commit that other (newer) branch is pointing to
	- Branch being marged must be *ahead* of checked out branch
- Regular merge
	- Two divergent branches are combined
	- Merge commit is created

#### Merge Conflicts

- Will occur if exact same lines are changed in separate branches
- `git status`
	- Shows in which file merge conflict occurs
- Merge conflict indicators
	- `<<<<<<< HEAD` everything below this line (until next indicator) shows you what's on current branch
	- `||||||| merged common ancestors` everything below this line (until next indicator) shows you what original lines were
	- `=======` is end of original lines, everything that follows (until next indicator) is what's on branch that's being merged in
	- `>>>>>>> heading-update` is ending indicator of what's on branch that's being merged in (in this case, heading-update branch)
	- Indicators have to be removed manually

```
$ git merge heading
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit result.
```

### Undoing Changes

- `git commit --amend`
	- Alter most recent commit
	- Ensure that working directory is clean, no uncommited changes in repository
	- Code editor opens and allows to change commit message
	- Add files to recent commit
		- Save files and stage modified files
		- Run command
		- Most recent commit will be updated, no new commit
- `git revert ac3f78`
	- Reverses commit with SHA ac3f78
	- Will undo changes that were made by provided commit
	- Takes changes made in commit and does exact opposite
	- Creates new commit to record change
- `git reset HEAD~1`
	- Erases parent of current commit
	- Moves head and "master" to previous commit
	- `git reset --mixed HEAD~1` is default, `--mixed` can be avoided, unstages committed changes, moves to working directory
	- `git reset --soft HEAD~1` moves committed changes to staging index
	- `git reset --hard HEAD~1` erases commit
	- Referencing commit
		- `HEAD^`, `HEAD~`, `HEAD~1` to reference parent commit of current
		- `HEAD^^`, `HEAD~2` to reference grandparent commit of current
		- `HEAD^^^`, `HEAD~3` to reference great-grandparent commit of current
	- Advised to great backup branch before resetting

## Remote Repositories

- GitHub as service for hosting version control repositories
- Distributed version control system: Not *one* main repository, each developer has copy
- Send copy of local repository to GitHub as remote repository
- "Origin" is name of main repository, possible to rename, but typically left as it is
- `git remote`
	- Returns short name of remote repository
- `git remote -v`
	- Returns full path of remote repository
	- Used to verify connection
- `git remote add origin https://github.com/username/name.git`
	- Creates connection to remote repository
	- "Origin" set short name for project, can be anything
- `git push origin master`
	- Sends local commits to remote repository
	- Replace "origin" with respective short name
	- Repace "master" with respective branch name
- `git pull origin master`
	- Retrieves updates from remote repository and merges
	- Marker "origin/master" is called tracking branch, includes short name and branch
	- If change is made to remote repository by someone else, "origin/master" tracking branch in local repository will not move
- `git fetch origin master`
	- Use if there are commits on remote repository but also on local repository that are not in sync
	- Retrieves commits from remote repository but does not automatically merges local branch with remote tracking branch
	- Commits on remote branch are copied to local repository, but local branch does not change
	- Merge manually by `git merge origin/master` to bring remote changes to local "master" branch
	- Followed by `git push origin master` to update remote repository with commits made locally
- `git clone https://github.com/username/name`
	- Targets existing repository and creates local clone in current directory
- Forking
	- Creates identical copy of original repository
	- Fork repository to own account allowing full control over repository
	- Button on GitHub repository page

```
$ git remote -v
origin	https://github.com/udacity/course-git-blog-project (fetch)
origin	https://github.com/udacity/course-git-blog-project (push)
```

```
$ git push origin master
Username for 'https://github.com': username
Password for 'https://username@github.com':
Counting objects: 6, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 966 bytes | 966.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To https://github.com/username/name.git
 * [new branch]      master -> master
```

```
$ git log --oneline --graph --all
* 4163680 (HEAD -> master, origin/master) Initial
```

```
$ git pull origin master
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), done.
From https://github.com/username/name
 * branch            master     -> FETCH_HEAD
   4163680..23e1e65  master     -> origin/master
Updating 4163680..23e1e65
Fast-forward
 css/app.css | 5 +++++
 1 file changed, 5 insertions(+)
```

```
$ git clone https://github.com/username/name
Cloning into 'course-collaboration-travel-plans'...
remote: Counting objects: 24, done.
remote: Total 24 (delta 0), reused 0 (delta 0), pack-reused 24
Unpacking objects: 100% (24/24), done.
```

- `git shortlog`
	- Displays commits sorted by author
	- Flag `-s` shows number of commits by each developer and `-n` sorts them numerically
- `git log -author="name"`
	- Filters commits by provided author
- `git log --grep="bug"` or `git log --grep "bug"`
	- Filter down to commits that reference "bug"
	- "Grep" is pattern matching tool
- `git rebase -i HEAD~3` or `git rebase -i 9b1549d`
	- Powerful command
	- Allows to squash, meaning to combine, multiple commits together
	- Last three commits are combined or SHA as base

## Request And Responses

### Web Server

- Install Ncat, part of Nmap, network testing toolkit
	- [Mac Download](https://nmap.org/dist/nmap-7.30.dmg)
	- [Windows Download](https://nmap.org/dist/nmap-7.30-setup.exe)
- Test installation
	- Open two terminals
	- Run `ncat -l 9999` in one, runs as server, listens on port 9999
	- Run `ncat localhost 9999` in secondary, runs as client, connects to localhost
	- Type something in each terminal, should appear on other terminal
- Python `http.server`module can run built-in web server on computer
  - Run `python3 -m http.server 8000`
  - Access http://localhost:8000 through browser

 ```
 $ python3 -m http.server 8000
 Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
 ```

### URI

- URI: Uniform Resource Identifier
- URL: Uniform Resource Locator
- `https://en.wikipedia.org/wiki/Fish`
- Consists of
	- Scheme like http:, https:, file:, mailto:
	- Hostname like //google.com, //localhost, //216.58.194.174/
	- Path like /Fish, / search?q=ponies
	- Query like ?q=fish
	- Fragment like #Discovery

### Hostnames

- Hostname will be looked up and uses Domain Name Service (DNS) to translate hostname into IP address
- `host www.google.com` or `nslookup www.google.com` to look up IP address
- 127.0.0.1 is computers own IPv4 address, ::1 for IPv6

```
$ host www.google.com
www.google.com has address 172.217.17.36
www.google.com has IPv6 address 2a00:1450:400e:804::2004
```

### Ports

- IP addresses distinguish computers, port numbers distinguish programs on computers
- When client connects to port and sends request, operating system knows to forward request to server that is listening on that port

### Requests

`127.0.0.1 - - [03/Oct/2016 15:45:50] "GET /readme.png HTTP/1.1" 200 -``

- `GET` is method or HTTP verb to request resource
- `/readme.png` is path of resource
- `HTTP/1.1` is protocol of request

```
GET / HTTP/1.1
Host: google.com
```

### Responses

- Status line
	- Shows whether understood and resource available
	- Three digit number is status code
		- 1xx — informational
		- 2xx — success
		- 3xx — redirection
		- 4xx — client error
		- 5xx — server error
- Headers
	- Can include multiple
	- Start with keyword like location, content-type or set-cookie
		- `Content-type: text/html; charset=utf-8` tells client that response body is HTML document written in UTF-8 text
- Response body
	- Copy of requested resource or error message

## Web From Python

- Run web service
- Example below is HTTP server that responds to GET request by sending back greeting, runs in terminal access server at http://localhost:8000
- Import modules
- Handler class inherits from `BaseHTTPRequestHandler` parent class as defined in `http.server`
- `do_GET` handles GET requests
- Handler parent class contains methods to send status code, headers, response body
- `self.wfile` used to send response, `wfile`stands for *writeable file*

```
from http.server import HTTPServer, BaseHTTPRequestHandler

class HelloHandler(BaseHTTPRequestHandler):
    def do_GET(self):
        # First, send 200 OK response.
        self.send_response(200)

        # Then send headers.
        self.send_header('Content-type', 'text/plain; charset=utf-8')
        self.end_headers()

        # Now, write response body.
        self.wfile.write("Hello, HTTP!\n".encode())

if __name__ == '__main__':
    server_address = ('', 8000)  # Serve on all addresses, port 8000.
    httpd = HTTPServer(server_address, HelloHandler)
    httpd.serve_forever() # Server starts and keeps running
```

```
self.wfile.write(self.path.encode())
# Server echoes back requested path it receives
```

- `.encode()` translates strings to bytes objects
	- HTTP response can contain any kind of data but `self.wfile.write` method expects to be given bytes object
	- Old software tended to assume that each character takes up only one byte but this does not apply for other languages like Chinese, hence, encoding is required
	- Most common encoding is UTF-8 which is default in python and supports characters which may represent one to four bytes depending on language

```
>>> len('cat'.encode())
3
>>> len('ねこ'.encode())
6
```

### Queries And Quoting

- Example: https://www.google.com/search?q=gray+squirrel&tbm=isch
- Query part is after `&``, written as `key=value`, separated by `&``
	- Example has query paramters `q` and `tbm` with values `gray+squirrel` and `isch`
- Python library `urllib.parse` can unpack parameters
- URL quoting translates string into form without special characters and spaces so that HTTP URL can handle it
	- Equivalent to URL-encoding or URL-escaping
	- Spaces translated into plus signs
	- `gray+squirrel` becomes `gray squirrel`


```
>>> from urllib.parse import urlparse, parse_qs
>>> address = 'https://www.google.com/search?q=gray+squirrel&tbm=isch'
>>> parts = urlparse(address)
>>> print(parts)
ParseResult(scheme='https', netloc='www.google.com', path='/search', params='', query='q=gray+squirrel&tbm=isch', fragment='')
>>> print(parts.query)
q=gray+squirrel&tbm=isch
>>> query = parse_qs(parts.query)
>>> query
{'q': ['gray squirrel'], 'tbm': ['isch']}
```

### Forms

- With `GET` method, browser puts all form fields into URL and sends it to server as query in request path
	- User can bookmark resulting page
	- Fine for search engines but not to alter or create resource
	- Results in idempotent action, meaning doing it second time just shows same result

```
<!DOCTYPE html>
<title>Login Page</title>
<form action="http://localhost:8000/" method="GET">
<label>Username:
  <input type="text" name="username">
</label>
<br>
<button type=submit>Log in!</button>
```

`127.0.0.1 - - [10/Oct/2017 18:08:02] "GET /?username=Max&pw=1234 HTTP/1.1" 200 -`

- `POST` method
	- Not idempotent action, confirm resubmitting form
	- Form data will not be encoded in URI path, instead data is in request body

```
<!DOCTYPE html>
<title>Testing POST requests</title>
<form action="http://localhost:9999/" method="POST">
  <label>Magic input:
    <input type="text" name="magic" value="mystery">
  </label>
  <br>
  <button type="submit">Do thing!</button>
</form>
```

- Within `do_POST` method, read request body by calling `self.rfile.read` method
	- `self.rfile.read(140)` reads 140 bytes
	- `self.header`is object that acts like dictionary and holds key `Content-length` that returns length of request body in bytes
	- If body is empty `self.headers['content-length']` will crash with key error
	- Instead use `.get` dictionary to get header value safely
- `urllib.parse.parse_qs` to extract POST parameters

```
length = int(self.headers.get('Content-length', 0))
data = self.rfile.read(length).decode()
```

```
from http.server import HTTPServer, BaseHTTPRequestHandler
from urllib.parse import parse_qs

class MessageHandler(BaseHTTPRequestHandler):
    def do_POST(self):
        # How long was message?
        length = int(self.headers.get('Content-length', 0))

        # Read correct amount of data from request.
        data = self.rfile.read(length).decode()

        # Extract "message" field from request data.
        message = parse_qs(data)["message"][0]

        # Send "message" field back as response.
        self.send_response(200)
        self.send_header('Content-type', 'text/plain; charset=utf-8')
        self.end_headers()
        self.wfile.write(message.encode())

if __name__ == '__main__':
    server_address = ('', 8000)
    httpd = HTTPServer(server_address, MessageHandler)
    httpd.serve_forever()
```

### Post-Redirect-Get Pattern

- Clients `POST` to server or create resource, server replies `200 OK` on success but with `303` redirect, redirect causes client to `GET`created resource
- Advantage is every page is part of `GET` request and can be bookmarked and reloaded without resubmitting

#### Messageboard

- Go to http://localhost:8000/
- Browser sends `GET` request and server replies with `200 OK` and html
- Form appears with list of existing comments if available
- User writes comment and submits, browser sends comment via `POST` to server
- Server updates list of comments and replies with `303` redirect setting `Location: /` header to tell browser to request main page via `GET`
- Redirect response causes browser to go back to same page user started sending `GET` request which replies with `200 OK` and HTML

```
from http.server import HTTPServer, BaseHTTPRequestHandler
from urllib.parse import parse_qs

memory = []

form = '''<!DOCTYPE html>
  <title>Message Board</title>
  <form method="POST">
    <textarea name="message"></textarea>
    <br>
    <button type="submit">Post it!</button>
  </form>
  <pre>
{}
  </pre>
'''

class MessageHandler(BaseHTTPRequestHandler):
    def do_POST(self):
        # How long was message?
        length = int(self.headers.get('Content-length', 0))

        # Read and parse message
        data = self.rfile.read(length).decode()
        message = parse_qs(data)["message"][0]

        # Escape HTML tags in message so users can't break world+dog.
        message = message.replace("<", "&lt;")

        # Store it in memory.
        memory.append(message)

        # Send 303 back to root page.
        self.send_response(303)  # redirect via GET
        self.send_header('Location', '/')
        self.end_headers()

    def do_GET(self):
        # First, send 200 OK response.
        self.send_response(200)

        # Then send headers.
        self.send_header('Content-type', 'text/html; charset=utf-8')
        self.end_headers()

        # Send form with messages in it.
        mesg = form.format("\n".join(memory))
        self.wfile.write(mesg.encode())

if __name__ == '__main__':
    server_address = ('', 8000)
    httpd = HTTPServer(server_address, MessageHandler)
    httpd.serve_forever()
```

### Requests

- `requests` library for sending requests to web servers and interpreting responses
- Run `pip3 install requests` to install library
- Sending request returns `Response` object

```
>>> import requests
>>> abc = requests.get('http://www.udacity.com')
>>> abc
<Response [200]>
>>> type(a)
<class 'requests.models.Response'>
```

## JSON

- Data format based on syntax of JavaScript often used for web-based APIs
- Many services allow sending HTTP queries and return structured data in JSON format
- Python has built-in module to translate JSON to Python dictionary
- Example is Star Wars API containing information about character

```
>>> abc = requests.get('http://swapi.co/api/people/1/')
>>> abc.json()['name']
'Luke Skywalker'
```

```
import requests

def SampleRecord():
    r = requests.get("http://uinames.com/api?ext&region=United%20States",
                     timeout=2.0)
    j = r.json()

    return "My name is {} {} and PIN on my card is {}.".format(
        j["name"],
        j["surname"],
        j["credit_card"]["pin"]
    )

if __name__ == '__main__':
    print(SampleRecord())
```

## Deploying To Hosting Service

- Create new separate Git repository with code
- Connect to [Heroku](https://heroku.com/)
	- Heroku enables to build, run and operate applications in cloud
	- Install Heroku [command-line interface](https://devcenter.heroku.com/articles/heroku-cli) (CLI)
	- Test with `heroku` command
	- `heroku login` to authenticate
- Create configuration files
	- Required for deployment
	- `runtime.txt` tells Python version to run, [currently supported versions](https://devcenter.heroku.com/articles/python-runtimes)
	- `requirements.txt` used by Heroku to install dependencies of application that are not in Python standard library like requests module
	- `Procfile` used by Heroku to specify command line for running applications
- Listen on configurable port
	- Heroku needs to be able to tell server what port to listen on
	- Set up environment variable that is passed to server from program that starts it
	- Python can access environment variables in `os.environ` dictionary
	- Call environment variable `PORT`
	- `import os` to access `os.environ`
- Create app
	- `heroku create your-app-name` to tell Heroku about app and name it
	- https://your-app-name.herokuapp.com/
- Push app
	- `git push heroku master` to deploy
- Check server logs if issues

```
if __name__ == '__main__':
    port = int(os.environ.get('PORT', 8000))   # Use PORT if it's there.
    server_address = ('', port)
    httpd = http.server.HTTPServer(server_address, Shortener)
    httpd.serve_forever()
```

## Concurrency

- Being able to handle two ongoing tasks at same time, basik `http.server.HTTPServer` does not have it
- Python standard library supports by adding *mixin* to `HTTPServer` class

```
import threading
from socketserver import ThreadingMixIn

class ThreadHTTPServer(ThreadingMixIn, http.server.HTTPServer):
    "This is HTTPServer that supports thread-based concurrency."
```

```
if __name__ == '__main__':
    port = int(os.environ.get('PORT', 8000))
    server_address = ('', port)
    httpd = ThreadHTTPServer(server_address, Shortener)
    httpd.serve_forever()
```

## Specialized Web Server Programs

- Apache, Nginx, IIS more advanced web server than Python http.server
- Build for large number of requests
- Allow routing meaning to dispatch requests to particular backend server
- Load balancing meaning to split up requests among several servers
- Can cache meaning to temporarily store resources that are likely to be reused to respond faster

## Cookies

- Retained piece of information in browser that can be send back to server when browser makes request
- `SimpleCookie` class to create cookie

```
from http.cookies import SimpleCookie, CookieError

out_cookie = SimpleCookie()
out_cookie["bearname"] = "Smokey Bear"
out_cookie["bearname"]["max-age"] = 600 # How long cookie lasts in seconds.
out_cookie["bearname"]["httponly"] = True #Alternative "secure" for HTTPS only
```

- `self.send_header("Set-Cookie", out_cookie["bearname"].OutputString())`
	- Sends cookie as header from request handler
- `in_cookie = SimpleCookie(self.headers["Cookie"]) in_data = in_cookie["bearname"].value`
	- Reads incoming cookies
- It is possible for user to modify cookie value, toolkits like Flask or Rail cryptographically sign cookies so that they will not be accepted if modified
- If cookie data is displayed as HTML, be careful to escape any HTML specific characters that might be in it
	- Use Python `html.escape` function

## HTTPS

- Follows encrypted connection called Transport Layer Security (TLS) or Secure Sockets Layer (SSL) through public-key cryptography
- Keeps connection private by encrypting everything sent over it
- Browser can authenticate server and ensure that response is from actual server that has been requested
- Helps to protect integrity of data sent over that connection checking that it has not been modified or replaced

## Other HTTP Methods

- Unlike `GET` and `POST`, usage of other methods is not built into normal operations of web browsers
	- For other methods, server-side code to accept it and client-side JavaScript code to make use of it has to be written
- `PUT` for creating resources but most file upload are done through `POST` method
- `DELETE` removes resource from server
- `PATCH`for making changes in well-defined way
- `HEAD`, `OPTIONS`, `TRACE` for debugging
- Methods surprising effect: Organization put up web site where "edit" and "delete" actions happened through `GET`request, as result, next search-engine crawler that came along [deleted whole site](http://thedailywtf.com/articles/The_Spider_of_Doom)

## New Developments

- HTTP/2 is new version of HTTP
- Python libraries are not mature yet
- Demo
	- [Gophertiles](https://http2.golang.org/gophertiles) demo can load same web page over HTTP/1.1 and HTTP/2 and can extra latency to request
	- Use [supported browser](http://caniuse.com/#feat=http2)

## Resources

- Point before file name implies that file is invisible on Mac/Linux
	- `defaults write com.apple.finder AppleShowAllFiles YES` in terminal
	- Press <kbd>Option</kbd>, right click Finder icon and select relaunch
	- Files will be shown
	- `defaults write com.apple.finder AppleShowAllFiles NO` in terminal to hide
- View file extensions on Mac
	- Open Preferences in Finder, go to Advanced
	- Check "Show all filename extensions"
- Setting up repository: [Atlassian](https://www.atlassian.com/git/tutorials/setting-up-a-repository)
- Inspecting repository: [Atlassian](https://www.atlassian.com/git/tutorials/inspecting-a-repository)
- Associating text editors with Git: [GitHub Help](https://help.github.com/articles/associating-text-editors-with-git/)
- Udacity Commit Message Style Guide: [GitHub](https://udacity.github.io/git-styleguide/)
- Ignoring files: [GitHub](https://help.github.com/articles/ignoring-files/)
- Create .gitignore files: [Gitignore.io](https://www.gitignore.io)
- Using branches: [Atlassian](https://www.atlassian.com/git/tutorials/using-branches)
- Playful website: [Learn Git Branching](https://learngitbranching.js.org)
- Git merge: [Atlassian](https://www.atlassian.com/git/tutorials/git-merge)
- Beginner’s Git and GitHub Tutorial: [Udacity](https://blog.udacity.com/2015/06/a-beginners-git-github-tutorial.html)
- Try Git: [GitHub](https://try.github.io)
- [Git Immersion](http://gitimmersion.com)
- Open Source projects for newbies: [First Timers Only](http://www.firsttimersonly.com)
- Desktop App for Learning Git and GitHub: [Git-it](https://github.com/jlord/git-it-electron)
- Tasks for new contributors: [Up For Grabs](http://up-for-grabs.net/#/)
- [First Pull Request](http://firstpr.me/)
- URL schemes: [Iana](http://www.iana.org/assignments/uri-schemes/uri-schemes.xhtml)
- Python classes: [Docs](https://docs.python.org/3/tutorial/classes.html)
- Python Unicode How To: [Docs](https://docs.python.org/3.6/howto/unicode.html)
- Python parse URL into components: [Docs](https://docs.python.org/3/library/urllib.parse.html)
- Python requests: [Doc](http://docs.python-requests.org/en/master/user/quickstart/)
- Introducing JSON: [JSON](http://www.json.org)
- Fake names and accounts for designs and mockups: [UI Names](http://uinames.com/)
- HTTP Methods: [W3](https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html)
- HTML/2: [GitHub](https://http2.github.io/faq/)
- Tutorials and reference materials on HTTP: [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTTP)
- Create own HTTPS certificates and install them on site: [Let's Encrypt](https://letsencrypt.org)
- Chrome extension that shows headers and request information of every browser request: [HTTP Spy](https://chrome.google.com/webstore/detail/http-spy/agnoocojkneiphkobpcfoaenhpjnmifb?hl=en)

# Backend: Databases And Application

## Install Virtual Machine

- Linux server that runs locally to run SQL database server and web app

### Set Up Terminal

- Terminal for Mac and Linux
- install Git Bash on Windows from [Git-SCM](https://git-scm.com/downloads)

### Install VirtualBox

- Runs virtual machine
- Download from [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Install *platform package*, extension pack or SDK not required

### Install Vagrant

- Configures virtual machine and allows file sharing between host computer and virtual machine's file system
- Download from [Vagrant](https://www.vagrantup.com/downloads.html)
- Allow network permissions or make firewall exception on Windows
- Run `vagrant --version` in terminal, shows version number if successful

### Configure And Start Virtual Machine

- Get configuration by forking and cloning [repository](https://github.com/udacity/fullstack-nanodegree-vm)
- Change directory to "vagrant" directory inside
- Run `vagrant up` which causes Vagrant to download Linux operating system and install it
- Run `vagrant ssh` upon completion to log in to newly installed Linux virtual machine
- Files in "vagrant" directory are shared with vagrant folder on computer
- `cd /vagrant` if required
- PostgreSQL database server will automatically start
- `psql databasename` to access it and run SQL statements
- `exit` or <kbd>Ctrl</kbd> + <kbd>D</kbd> to log out
- If computer reboot, virtual machine needs to be restarted

```
vagrant=> select 2+2 as sum;
 sum
-----
   4
(1 row)
```

## Python DB-API

- Connect Python to SQL database with DB-API calls
- Each database system has own DB-API module
	- For SQLite use sqlite3 library
	- For PostgreSQL use psycopg2 library
	- For ODBC use pyodbc library
	- For MySQL use mysql.connector library
- When insert query, changes need to be commited with `.commit` method on connection or `.rollback`
- Changes are rolled back if connection gets closed without commit
- Atomicity
	- Transaction happens as whole or not at all
	- No half written changes are made when code crashes

```
import sqlite3

# Connect to database "students" or specify connection string, db returns connection object.
db = sqlite3.connect("students")
# Cursor runs queries and fetches results.
c = db.cursor()
query = "SELECT name, id FROM students;"
# Execute query using cursor.
c.execute(query)
Fetch results with fetchall() or fetchone()
rows = c.fetchall()

# Return raw data.
print "Row data:"
print rows

# Print one column only.
print
print "Student names:"
for row in rows:
  print "  ", row[0]

# Close to safe resources.
db.close()
```

### Reference

- `module.connect(...)`
	- Connect to database, arguments to connect differ from module to module; see documentation for details, connect returns Connection object or raises exception
- For methods below, note that you don't literally call (for instance) `Connection.cursor()` in your code, you make Connection object, save it in variable (maybe called db) and then call `db.cursor()`
- `Connection.cursor()`
	- Makes Cursor object from connection, cursors are used to send SQL statements to database and fetch results
- `Connection.commit()`
	- Commits changes made in current connection, you must call commit before closing connection if you want changes (such as inserts, updates, or deletes) to be saved, uncommitted changes will be visible from your current connection, but not from others
- `Connection.rollback()`
	- Rolls back (undoes) changes made in current connection, you must roll back if you get exception if you want to continue using same connection
- `Connection.close()`
	- Closes connection, connections are always implicitly closed when your program exits, but it's good idea to close them manually especially if your code might run in loop
- `Cursor.execute(statement)`
	- `Cursor.execute(statement, tuple)`
	-	Execute SQL statement on database, if you want to substitute variables into SQL statement, use second form — see documentation for details
- If your statement doesn't make sense (like if it asks for column that isn't there), or if it asks database to do something it can't do (like delete row of table that is referenced by other tables' rows) you will get exception
- `Cursor.fetchall()`
	- Fetch all results from current statement
- `Cursor.fetchone()`
	- Fetch just one result, returns tuple, or none if there are no results

## Running Form

- Start virtual machine with `vagrant up`
- Log in to virtual machine with `vagrant ssh`
- `cd /vagrant` if required
- Go to directory

```
vagrant@vagrant:/vagrant/forum$ python forum.py
 * Running on http://0.0.0.0:8000/ (Press CTRL+C to quit)
10.0.2.2 - - [11/Oct/2017 18:50:33] "GET / HTTP/1.1" 200 -
````

## PostgreSQL

- Sample empty database "name.sql"
	- `CREATE TABLE tablename ( content TEXT, time TIMESTAMP DEFAULT CURRENT_TIMESTAMP, id SERIAL );`
- `psql databasename` to log into database if database server is installed
- Or `psql -d databasename  -f filename.sql` to also run statements in file
- Database prompt appears allowing to run SELECT statements
- `\d tablename` to see contents of columns
- `\dt` to list all tables in database
- `\dt+` to list all tables plus additional information
- `\H` to switch between printing table in plain text and HTML
- `\q` to exit database
- `select * from tablename \watch` with out semicolon will display contents of table and refresh it every two seconds to see changes made, run in second terminal

## Security

- SQL insertion attack or Bobby Tables
	- Some of `POST` text is interpreted as database command, security bug
	- `%s` in query text without single quotation mark followed by tuple query parameter which will substitute `%s` to be safe against SQL injection attack
	- Make sure to use query parameters instead of string substitution
	- Never us Python string concatenation or string parameter interpolation to pass variables to SQL query string
	- [XKCD Comic](https://xkcd.com/327/)
- Script injection attack
	- Fix by avoiding to allow JavaScript code in input form
	- `bleach` Python library to clean input
	- Decide on whether to sanitize input or output

forumdb.py to edit database

```
import psycopg2, bleach

DBNAME = "forum"

def get_posts():
  """Return all posts from 'database', most recent first."""
  db = psycopg2.connect(database=DBNAME)
  c = db.cursor()
  c.execute("select content, time from posts order by time desc")
  posts = c.fetchall()
  db.close()
  return posts

def add_post(content):
  """Add post to 'database' with current timestamp."""
  db = psycopg2.connect(database=DBNAME)
  c = db.cursor()
  c.execute("insert into posts values (%s)", (content,))  # Better, but ...
  db.commit()
  db.close()
```

forum.py as main

```
from flask import Flask, request, redirect, url_for

from forumdb_initial import get_posts, add_post

app = Flask(__name__)

# HTML template for forum page
HTML_WRAP = '''\
<!DOCTYPE html>
<html>
  <head>
    <title>DB Forum</title>
    <style>
      h1, form { text-align: center; }
      textarea { width: 400px; height: 100px; }
      div.post { border: 1px solid #999;
                 padding: 10px 10px;
                 margin: 10px 20%%; }
      hr.postbound { width: 50%%; }
      em.date { color: #999 }
    </style>
  </head>
  <body>
    <h1>DB Forum</h1>
    <form method=post>
      <div><textarea id="content" name="content"></textarea></div>
      <div><button id="go" type="submit">Post message</button></div>
    </form>
    <!-- post content will go here -->
%s
  </body>
</html>
'''

# HTML template for individual comment
POST = '''\
    <div class=post><em class=date>%s</em><br>%s</div>
'''

@app.route('/', methods=['GET'])
def main():
  '''Main page of forum.'''
  posts = "".join(POST % (date, text) for text, date in get_posts())
  html = HTML_WRAP % posts
  return html

@app.route('/', methods=['POST'])
def post():
  '''New post submission.'''
  message = request.form['content']
  add_post(message)
  return redirect(url_for('main'))

if __name__ == '__main__':
  app.run(host='0.0.0.0', port=8000)
```

## CRUD

- Create, read, update and delete
- ORM: Object-relational mapping
	- Translates between Python code and SQL for database
	- SQL Alchemy is open source ORM for Python

### SQL Alchemy

- Coding components
	- Configuration: imports necessary modules and sets dependencies, creates instance of declarative base
	- Class: representation of table as python class, extends `Base` class, table and mapper code nested inside
	- Table: represents table
	- Mapper: connects column to class, creates variables used to create columns in database, includes attributes
- Pre installed in Vagrant

```
import os
import sys
from sqlalchemy import Column, ForeignKey, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import relationship
from sqlalchemy import create_engine

Base = declarative_base()

class Restaurant(Base):
    __tablename__ = 'restaurant'

    id = Column(Integer, primary_key=True)
    name = Column(String(250), nullable=False)

class MenuItem(Base):
    __tablename__ = 'menu_item'

    name = Column(String(80), nullable=False)
    id = Column(Integer, primary_key=True)
    description = Column(String(250))
    price = Column(String(8))
    course = Column(String(250))
    restaurant_id = Column(Integer, ForeignKey('restaurant.id'))
	# 'restaurant.id' refers to id in restaurant table, foreign key relationship
    restaurant = relationship(Restaurant)
	# Creates relationship to class restaurant

engine = create_engine('sqlite://restaurantmenu.db')

Base.metadate.create_all(engine)
# Adds classes as tables in database
```

- Add data to empty database

```
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
# Import classes from file
from database_setup import Base
# Connect to database
engine = create_engine('sqlite:///restaurantmenu.db')
# Bind engine to base class, connects class definitions and corresponding tables
Base.metadata.bind = engine
# Connect code execution to engine
DBSession = sessionmaker(bind = engine)

# DBSession is staging zone, not realised until committed
session = DBSession()
myFirstRestaurant = Restaurant(name="Pizza Palace")
# Add to staging zone and commit to store in database
session.add(myFirstRestaurant)
session.commit()

cheesepizza = MenuItem(name="Cheese Pizza", description="Made with all natural ingredients and fresh mozzarella", course="Entree", price="$8.99", restaurant = myFirstRestaurant)
session.add(cheesepizza)
session.commit()

# Finds restaurant table and return all entires in list
session.query(Restaurant).all()

firstResult = session.query(Restaurant).first()
# firstResult.name returns name of first restaurant in database

items = session.query(MenuItem).all()
for item in items:
	print item.name
# Returns names of each item in database
```

- Update database_setup

```
veggieBurgers = session.query(MenuItem).filter_by(name = 'Veggie Burger')
for veggieBurger in veggieBurgers:
	print veggieBurger.id
	print veggieBurger.price
	print veggieBurger.restaurant.name
	print "\n"
# Returns list of all Veggie Burgers in database

UrbanVeggieBurger = session.query(MenuItem).filter_by(id = 8).one()
print UrbanVeggieBurger.price

UrbanVeggieBurger.price = '$2.99'
session.add(UrbanVeggieBurger)
session.commit()

for veggieBurger in veggieBurgers:
	if veggieBurger.price != '$2.99':
		veggieBurger.price = '$2.99'
		session.add(veggieBurger)
		session.commit()
```

- Delete items

```
spinach = session.query(MenuItem).filter_by(name = 'Spinach Ice Cream').one()
print spinach.restaurant.names
session.delete(spinach)
session.commit()
```

## Running Web Servers

```
from BaseHTTPServer import BaseHTTPRequestHandler, HTTPServer

class WebServerHandler(BaseHTTPRequestHandler):

    def do_GET(self):
        if self.path.endswith("/hello"):
            self.send_response(200)
            self.send_header('Content-type', 'text/html')
            self.end_headers()
            message = ""
            message += "<html><body>Hello!</body></html>"
            self.wfile.write(message)
            print message
            return
        else:
            self.send_error(404, 'File Not Found: %s' % self.path)

def main():
    try:
        port = 8080
        server = HTTPServer(('', port), WebServerHandler)
        print "Web Server running on port %s" % port
        server.serve_forever()
    except KeyboardInterrupt:
        # Built in exception triggered when user holds ^C on keyboard
        print " ^C entered, stopping web server...."
        server.socket.close()

# Immediately run main method when interpreter runs script
if __name__ == '__main__':
    main()
```

- Execute `python webserver.py` from inside Vagrant
- Visit `localhost:8080/hello` with respective port
- Vagrant machine shows GET request and reply
- Added POST functionality below

```
from BaseHTTPServer import BaseHTTPRequestHandler, HTTPServer
import cgi

class webServerHandler(BaseHTTPRequestHandler):

    def do_GET(self):
        try:
            if self.path.endswith("/hello"):
                self.send_response(200)
                self.send_header('Content-type', 'text/html')
                self.end_headers()
                output = ""
                output += "<html><body>"
                output += "<h1>Hello!</h1>"
                output += '''<form method='POST' enctype='multipart/form-data' action='/hello'><h2>What would you like me to say?</h2><input name="message" type="text" ><input type="submit" value="Submit"> </form>'''
                output += "</body></html>"
                self.wfile.write(output)
                print output
                return

            if self.path.endswith("/hola"):
                self.send_response(200)
                self.send_header('Content-type', 'text/html')
                self.end_headers()
                output = ""
                output += "<html><body>"
                output += "<h1>&#161 Hola !</h1>"
                output += '''<form method='POST' enctype='multipart/form-data' action='/hello'><h2>What would you like me to say?</h2><input name="message" type="text" ><input type="submit" value="Submit"> </form>'''
                output += "</body></html>"
                self.wfile.write(output)
                print output
                return

        except IOError:
            self.send_error(404, 'File Not Found: %s' % self.path)

    def do_POST(self):
        try:
            self.send_response(301)
            self.send_header('Content-type', 'text/html')
            self.end_headers()
            ctype, pdict = cgi.parse_header(
                self.headers.getheader('content-type'))
            if ctype == 'multipart/form-data':
                fields = cgi.parse_multipart(self.rfile, pdict)
                messagecontent = fields.get('message')
            output = ""
            output += "<html><body>"
            output += " <h2> Okay, how about this: </h2>"
            output += "<h1> %s </h1>" % messagecontent[0]
            output += '''<form method='POST' enctype='multipart/form-data' action='/hello'><h2>What would you like me to say?</h2><input name="message" type="text" ><input type="submit" value="Submit"> </form>'''
            output += "</body></html>"
            self.wfile.write(output)
            print output
        except:
            pass

def main():
    try:
        port = 8080
        server = HTTPServer(('', port), webServerHandler)
        print "Web Server running on port %s" % port
        server.serve_forever()
    except KeyboardInterrupt:
        print " ^C entered, stopping web server...."
        server.socket.close()

if __name__ == '__main__':
    main()
```

## Flask

```
from flask import Flask
app = Flask(__name__)


@app.route('/')
@app.route('/hello')
def HelloWorld():
    return "Hello World"

if __name__ == '__main__':
    app.debug = True
    app.run(host='0.0.0.0', port=5000)
```

- `@app.route('/')` is decorator function, once `/` or `/hello` is called, subsequent function, `HelloWorld()` in this case will be executed
- `app.debug = True` enables debug support, server will restart each time it notices code change
- Full Flask application example: [GitHub Udacity](https://github.com/udacity/Full-Stack-Foundations/tree/master/Lesson-3/Final-Flask-Application)

### Templates

- Create directory "templates" in same directory as Flask applications
- Create "menu.html" inside for example
- Example: [GitHub Udacity](https://github.com/udacity/Full-Stack-Foundations/tree/master/Lesson-3/Final-Flask-Application/templates)

### Styling

- Create directory "static" in same directory as Flask applications
- Create "styles.css" inside for example
- Example: [GitHub Udacity](https://github.com/udacity/Full-Stack-Foundations/tree/master/Lesson-3/Final-Flask-Application/static)

### JSON Responses

- Through `from flask import jsonify`
- Example: [GitHub Udacity](https://github.com/udacity/Full-Stack-Foundations/blob/master/Lesson-3/19_Responding-with-JSON/project.py)

```
@app.route('/restaurants/<int:restaurant_id>/menu/JSON')
def restaurantMenuJSON(restaurant_id):
    restaurant = session.query(Restaurant).filter_by(id=restaurant_id).one()
    items = session.query(MenuItem).filter_by(
        restaurant_id=restaurant_id).all()
    return jsonify(MenuItems=[i.serialize for i in items])
```

## Authentication Versus Authorization

- Authentication: Verifying that you are who you say you are
- Authorization: Do you have right access to resource?
- Most widely used standard for authorization is OAuth, open standard
- Open ID connect is built on top of OAuth
- OAuth 2.0 Playground: [Google Developers](https://developers.google.com/OAuthplayground/)

### Third Party Authorization

- OAuth providers: Google, Facebook, Amazon, GitHub, PayPal
  - [OAuth official website](https://OAuth.net/2/)
- Pro's
  - Outsource authentication handling to OAuth providers
  - Easier to register users
  - Less passwords for users to remember
- Con's
  - Users need to have third party account
  - Users don't trust your site, keep authentication scopes minimal
  - Limited/restricted internet access
  - Different authentication requirements

### Creating Google Sign In

- Create client ID and secret
  - Visit [Google Console](https://console.developers.google.com/apis) and log in
  - Create new project
  - Go to APIs & auth and select Credentials
  - Create new client ID
  - Edit client ID settings, add domain or http://localhost:5000 to authorized JavaScript origins
- Anti-forgery state tokens
  - Ensure to send only to user that came up with request
  - Support security of users

```
<head>
<!--LOAD PRE-REQUISITES FOR GOOGLE SIGN IN -->
   <script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js">
   </script>
   <script src="//apis.google.com/js/platform.js?onload=start"> </script>
<!-- END PRE-REQUISITES FOR GOOGLE SIGN IN -->
</head>

<body>
<!-- GOOGLE PLUS SIGN IN BUTTON-->
          <div id="signinButton">
          <span class="g-signin"
            data-scope="openid email"
            data-clientid="YOUR_CLIENT_ID_GOES_HERE.apps.googleusercontent.com"
            data-redirecturi="postmessage"
            data-accesstype="offline"
            data-cookiepolicy="single_host_origin"
            data-callback="signInCallback"
            data-approvalprompt="force">
          </span>
        </div>
<!--END GOOGLE PLUS SIGN IN BUTTON -->
</body>
```

- Full HTML script with added callback function: [GitHub Udacity](https://github.com/udacity/ud330/blob/master/Lesson2/step4/templates/login.html)
- Server side Python script: [GitHub Udacity](https://github.com/udacity/ud330/blob/master/Lesson2/step6/project.py)

### Local Permission System

- Files: [GitHub Udacity](https://github.com/udacity/ud330/tree/master/Lesson3/step3)

### Creating Facebook Sign In

- Register app on [Facebook Developers](https://developers.facebook.com/)
- Store secrets in JSON file, [Example](https://github.com/udacity/ud330/blob/master/Lesson4/step2/fb_client_secrets.json)
- In Facebook Login add domain or http://localhost:5000 to valid OAuth redirect URIs section
- Files: [GitHub Udacity](https://github.com/udacity/ud330/tree/master/Lesson4/step2)

## Web APIs

- Application Programming Interface
- Pysical layers and intermediate communication layers with application layer on top
- HTTP is application layer protocol on top, others are FTP, IMAP, POP, SSH
- Above application layer is web service layer which can determine format in that APIs are send and received
- For example Simple Object Access Protocol (SOAP) which uses XML
- Or Representational State Transfer (REST) is set of styles and guideline and leverages features of HTTP3, can be used with XML and JSON, easier to implement and more popular
- Message formatting layer formats information that is send and received
- Extensible Markup Language (XML) format looks similar to HTML
- Or JavaScript Object Notation (JSON) designed to resemble JavaScript code and has key value pairs, more popular amongst new APIs

### REST Constraints

1. Client - server separation
2. Stateless, each request is treated like it is client's first request, serves should not remember clients, use tokens otherwise
3. Cacheable response messages can be stored on client if information on servers has not changed since last request
4. Uniform interface between all client and server types
5. Layered system means that client can have access to endpoint that relies on other endpoint without having to know underlying implementations
6. Code on demand (optional) allows code to be send to client for execution

## Accessing Published APIs

### HTTP Request

- Header
- Request line consists of HTTP verb, URI, HTTP version number, example `GET /home.html HTTP/1.1`
- Optional request headers used to describe specific properties about request, appear in name-value pairs
- Blank line
- Body (optional)
- Additional information

### HTTP Response

- Header
- Status line consists of HTTP version, status code, reason phrase, example `HTTP/1.1 200 OK`
- Response headers (optional) in form of name-value pairs
- Blank line
- Body (optional)
- Requested data

### Sending API Requests With Postman And Curl

- Curl can send and receiving HTTP messages in command line
- [Getting Started with cURL](https://www.ethanmick.com/getting-started-with-curl/)
- [Curl Documentation](https://curl.haxx.se/docs/manpage.html)
- Postman, Chrome extension, has user interface, view and build HTTP messages
- Example APIs
- Google Maps API to get Latitude and Longitude for specific location
- Foursquare API to get recommendation at specific Latitude and Longitude
- Wikipedia API
- StackExchange API

### Requesting From Python Code

```
import httplib2
import json

def getGeocodeLocation(inputString):
    # Use Google Maps to convert location into Latitute/Longitute coordinates
    # FORMAT: https://maps.googleapis.com/maps/api/geocode/json?address=1600+Amphitheatre+Parkway,+Mountain+View,+CA&key=API_KEY
    google_api_key = "PASTE_YOUR_KEY_HERE"
    locationString = inputString.replace(" ", "+")
    url = ('https://maps.googleapis.com/maps/api/geocode/json?address=%s&key=%s'% (locationString, google_api_key))
    h = httplib2.Http()
    result = json.loads(h.request(url,'GET')[1])
    latitude = result['results'][0]['geometry']['location']['lat']
    longitude = result['results'][0]['geometry']['location']['lng']
    return (latitude,longitude)
```

```
from geocode import getGeocodeLocation
import json
import httplib2

import sys
import codecs
sys.stdout = codecs.getwriter('utf8')(sys.stdout)
sys.stderr = codecs.getwriter('utf8')(sys.stderr)

foursquare_client_id = "PASTE_CLIENT_ID_HERE"
foursquare_client_secret = "PASTE_CLIENT_SECRET_HERE"

def findARestaurant(mealType,location):
    #1. Use getGeocodeLocation to get latitude and longitude coordinates of location string.
    latitude, longitude = getGeocodeLocation(location)
    #2.  Use foursquare API to find nearby restaurant with latitude, longitude, and mealType strings.
    #HINT: format for url will be something like https://api.foursquare.com/v2/venues/search?client_id=CLIENT_ID&client_secret=CLIENT_SECRET&v=20130815&ll=40.7,-74&query=sushi
    url = ('https://api.foursquare.com/v2/venues/search?client_id=%s&client_secret=%s&v=20130815&ll=%s,%s&query=%s' % (foursquare_client_id, foursquare_client_secret,latitude,longitude,mealType))
    h = httplib2.Http()
    result = json.loads(h.request(url,'GET')[1])

    if result['response']['venues']:
        #3.  Grab first restaurant
        restaurant = result['response']['venues'][0]
        venue_id = restaurant['id']
        restaurant_name = restaurant['name']
        restaurant_address = restaurant['location']['formattedAddress']
        address = ""
        for i in restaurant_address:
            address += i + " "
        restaurant_address = address
        #4.  Get  300x300 picture of restaurant using venue_id (you can change this by altering 300x300 value in URL or replacing it with 'orginal' to get original picture
        url = ('https://api.foursquare.com/v2/venues/%s/photos?client_id=%s&v=20150603&client_secret=%s' % ((venue_id,foursquare_client_id,foursquare_client_secret)))
        result = json.loads(h.request(url, 'GET')[1])
        #5.  Grab first image
        if result['response']['photos']['items']:
            firstpic = result['response']['photos']['items'][0]
            prefix = firstpic['prefix']
            suffix = firstpic['suffix']
            imageURL = prefix + "300x300" + suffix
        else:
            #6.  if no image available, insert default image url
            imageURL = "http://pixabay.com/get/8926af5eb597ca51ca4c/1433440765/cheeseburger-34314_1280.png?direct"
        #7.  return dictionary containing restaurant name, address, and image url
        restaurantInfo = {'name':restaurant_name, 'address':restaurant_address, 'image':imageURL}
        print "Restaurant Name: %s" % restaurantInfo['name']
        print "Restaurant Address: %s" % restaurantInfo['address']
        print "Image: %s \n" % restaurantInfo['image']
        return restaurantInfo
    else:
        print "No Restaurants Found for %s" % location
        return "No Restaurants Found"

if __name__ == '__main__':
    findARestaurant("Pizza", "Tokyo, Japan")
    findARestaurant("Tacos", "Jakarta, Indonesia")
```

## Creating API Endpoints

- Example Code: [GitHub Udacity](https://github.com/udacity/APIs/tree/master/Lesson_3/06_Adding%20Features%20to%20your%20Mashup/Solution%20Code)

## API Securing

- Use `passlib.apps` to store hashes of passwords and not passwords themselves for security
- `custom_app_context` is based on SHA-256 hashing algorithm
- Build function `hash_password` and `verify_password`
- Implemented token-based authentication: [GitHub Udacity](https://github.com/udacity/APIs/tree/master/Lesson_4/07_Implementing%20Token-Based%20Authentication%20in%20Flask)
- OAuth 2.0 as alternative to signing up and remembering another password: [GitHub Udacity](https://github.com/udacity/APIs/tree/master/Lesson_4/10_Adding%20OAuth%202.0%20for%20Authentication)
- Rate limiting: [GitHub Udacity](https://github.com/udacity/APIs/tree/master/Lesson_4/12_Rate%20Limiting)
- Redis is open-source in-memory data structure that can be used as database and can keep track of requests

## Developer-Friendly APIs

- Developer-friendly documentation
- Include FAQ section
- Add API playground
- Use proper URIs
- `/puppies` better than `/getpuppies`
- Use plural rather than singular
- Implement versioning
- `/api/v1/puppies` and `/api/v2/puppies` so that old APIs do not break
- Communicate with developer
- Set up blogs and forums
- Have code available on GitHub
- Communicate bugs and outages

## Resources

- Passing parameters to queries: [Initd](http://initd.org/psycopg/docs/usage.html)
- Bleach documentation: [Docs](http://bleach.readthedocs.io/en/latest/)
- SQL Alchemy: [Documentation](http://www.sqlalchemy.org)
- Multiple menu items as Python script: [GitHub](https://github.com/udacity/Full-Stack-Foundations/blob/master/Lesson_1/lotsofmenus.py)
- Python BaseHTTPServer: [Documentation](https://docs.python.org/2/library/basehttpserver.html)
- Full Python web server code with CRUD operations: [GitHub Udacity](https://github.com/udacity/Full-Stack-Foundations/blob/master/Lesson-2/Objective-5-Solution/webserver.py)
- Url_for: [Flask Documentation](http://flask.pocoo.org/docs/0.10/quickstart/#url-building)
- Deployment Options: [Flask Documentation](http://flask.pocoo.org/docs/0.10/deploying/)
- Security: [Flask Documentation](https://pythonhosted.org/Flask-Security/)
- Restaurants and Menus Final Project Code: [GitHub Udacity](https://github.com/udacity/Full-Stack-Foundations/tree/master/Lesson-4/Final-Project)

# Frontend: JavaScript And AJAX

## Requests And APIs

- Load content without reloading, AJAX is one implementation
  - Example: Facebook loads more content if user scrolls down without refreshing
- AJAX: Asynchronous JavaScript And XML
- Asynchronous requests to load content, can occur in background without blocking page load or use
- Requests can be inspected in Chrome Developer Tools in Network tab
- Response can be found in tab "Response" below
- Necessary components for AJAX request: only URL, settings are optional
- HAR is HTTP archive format, JSON-formatted archive file format for logging web browser's interactions with site
- Combine multiple APIs pushes web and creates business
- Methods of AJAX requests
  - [jQuery.ajax()](http://api.jquery.com/jquery.ajax/)
  - [jQuery.getJSON()](http://api.jquery.com/jquery.getjson/)

## jQuery

```
function loadData() {

var $body = $('body');
var $wikiElem = $('#wikipedia-links);
var $greeting = $('#greeting')

// clear old data before new request

$wikiElem.text("");

// Google Street View API request

var streetStr = $('#street').val();
var cityStr = $('#city').val();
var address = streetStr + ', ' + cityStr;

var streetviewUrl =  'http://maps.googleapis.com/maps/api/streetview?size=600x400&location=' + address + '';
$body.append('<img class="bgimg" src="' + streetviewUrl + '">');

// New York Times request

var nytimesUrl = 'http://api.nytimes.com/svc/search/v2/articlesearch.json?q=' + cityStr + '&sort=newest&api-key=XXXXXXXXXX'

$.getJSON(nytimesURL, function(data) {

    $nytHeaderElem.text('New York Times Articles About ' + cityStr);
    articles = data.response.docs;
    for (var i = 0; i < articles.length; i++) {
        var article = articles[i];
        $nytElem.append('<li class="article">' + '<a href="' + article.web_url + '">' + article.headline.main + '</a>' + '<p>' + article.snippet + '</p>' + '</li>');
    };

}).error(function(e){
    $nytHeaderElem.text('New York Times Articles Could Not Be Loaded');
});
```

- JavaScript file
- Use jQuery objects, $ for variables has no meaning but used to identify jQuery objects
- $ used to select object, points to jQuery object
- String of object needed in parenthesis, # represents ID
- Google Street View API requires to include size and location
  - [Documentation](https://developers.google.com/maps/documentation/streetview/)
- OAuth to authenticate users for services like Facebook, only users with accounts can get data if it is not publicly accessible
- jQuery.error gets into effect if AJAX effect fails, error handling
- Chain method to end of request
- jQuery 1.8, .error() is deprecated, use .fail() instead
  - [jQuery.error Documentation](http://api.jquery.com/error/)

```
$('#my-elem').click(function(e) {
  // Element has been clicked... do stuff here
});
```

## Model, View, Octopus

- Separate code into buckets
- MVO, MVC, MVP or MVVM
- Model
  - Stores all data from server and user
- View
  - Everything user sees and interacts with
  - DOM elements, input elements, buttons, images
  - User interface
- Octopus, Controller, Presenter or ViewModel
  - Connects model and view
  - Provides separation of concerns
  - Allows to change view or model without disturbing other
  - Also called controller, view model, presenter
- Example Cat Clicker with MVO: [GitHub Udacity](https://github.com/udacity/ud989-cat-clicker-premium-vanilla)

## Knockout JS

- Organizational library
- Declarative bindings
  - Connect DOM and data
- Automatic UI refresh
  - Updates view when model changes
  - Can update model when elements in view such as input fields change
  - Two way bindings
- Dependency tracking
  - Can create relationship between parts of model and will update model data that depends on other model data when other model data changes

```
<div class='liveExample'>

    <div>You've clicked <span data-bind='text: numberOfClicks'>&nbsp;</span> times</div>

    <button data-bind='click: registerClick, disable: hasClickedTooManyTimes'>Click me</button>

    <div data-bind='visible: hasClickedTooManyTimes'>
        That's too many clicks! Please stop before you wear out your fingers.
        <button data-bind='click: resetClicks'>Reset clicks</button>
    </div>

</div>
```

```
var ClickCounterViewModel = function() {
    this.numberOfClicks = ko.observable(0);

    this.registerClick = function() {
        this.numberOfClicks(this.numberOfClicks() + 1);
    };

    this.resetClicks = function() {
        this.numberOfClicks(0);
    };

    this.hasClickedTooManyTimes = ko.computed(function() {
        return this.numberOfClicks() >= 3;
    }, this);
};

ko.applyBindings(new ClickCounterViewModel());
```

- Enter in console
- Create observable `var favNum = ko.observable(42)`
- Get value `favNum()`
- Change value `favNum(43)`
  - This runs code that changes value in view and model if dependency exists
- Get new value `favNum()`
- Run `console.dir(favNum)` to display properties specified JavaScript object
- Create observable array `ko.observableArray([1,2,3])`
- Use `console.log('test')` for testing

### Apply Bindings In New View Model

- In this case, model is defined in `ViewModel` function
- HTML shows only extract

```
var ViewModel = function() {
  this.clickCount = ko.observable(0);
  this.name = ko.observable('Tabby');
  this.incrementCounter = function() {
    this.clickCount(this.clickCount() + 1);
  };
}

ko.applyBindings(new ViewModel());
```

```
<div>
  <h2 data-bind="text: name"></h2>
  <div data-bind="text: clickCount"></div>
  <img src="" data-bind="click: incrementCounter, attr: {imgSrc}">
</div>
<script src="js/lib/knockout-3.2.0.js"></script>
<script src="js/app.js"></script>
```

### Computed Observables

- Computes itself based on other stored data

```
var ViewModel = function() {
  this.firstName = ko.observable('Bob');
  this.lastName = ko.observable('Smith');
  this.fullName = ko.computed(function() {
      return this.firstName() + " " + this.lastName();
  }, this);
  // Passing in 'this' as argument ensures that it can be used within. ko.computed
}
```

### Foreach Bindings

- Foreach will repeat `<li>` `</li>` for each of nicknames

```
<ul data-bind="foreach: nicknames">
  <li data-bind="text: $data"></li>
</ul>
```

### Separating Functions

- Taking out function from `ViewModel` function

```
var Cat = function() {
  this.clickCount = ko.observable(0);
  this.name = ko.observable('Tabby');
}

var ViewModel = function() {
  this.currentCat = ko.observable(new Cat());
  this.incrementCounter = function() {
    this.currentCate().clickCount(this.currentCate().clickCount() + 1);
  };
}

ko.applyBindings(new ViewModel());
```

```
<div>
  <h2 data-bind="text: currentCate().name"></h2>
  <div data-bind="text: currentCate().clickCount"></div>
  <img src="" data-bind="click: incrementCounter, attr: {currentCate().imgSrc}">
</div>
<script src="js/lib/knockout-3.2.0.js"></script>
<script src="js/app.js"></script>
```

### With And Binding Context

- Add `data-bind="with: currentCat"` to high level comprising div
- Then all `currentCat().` references in HTML below can be removed and also `currentCat().` references within `incrementCounter().` function
- For click binding of `incrementCounter` needs to be adjusted to `$parent.incrementCounter` so it runs on `ViewModel`
- `$parent` allows to get up and out of current scope or binding context
- Alternatively, set new variable `self` as `this`, in this case `self` will also refer to `ViewModel` function independent of `with` setting

```
var ViewModel = function() {
  var self = this;

  this.currentCat = ko.observable(new Cat());
  this.incrementCounter = function() {
    self.currentCate().clickCount(self.currentCate().clickCount() + 1);
  };
}
```

### Passing In Data

```
var Cat = function(data) {
  this.clickCount = ko.observable(data.clickCount);
  this.name = ko.observable(data.name);
  // data.clickCount and data.name will refer to values stored in function below.
}

var ViewModel = function() {
  this.currentCat = ko.observable(new Cat({
    clickCount: 0,
    name: 'Tabby'
    // Passing in values to cat constructor function above.
  }));
}
```

### Separated Dataset

```
var initialCat = [
{
  clickCount: 0,
  name: 'Tabby'
}
// Array of cat objects storing data.
]

var ViewModel = function() {
  var self = this;

  this.catList = ko.observableArray([]);
  // Cats stored in observable Array

  initialCats.forEach(function(catItem) {
    self.catList.push(new Cat(catItem));
  });
  // Loop over each initial cats and make new object. Pass each cat to catList created above.

  this.currentCat = ko.observable( this.catList()[0] );
  // Access first cat in list.

  this.incrementCounter = function() {
    self.currentCate().clickCount(self.currentCate().clickCount() + 1);
  };

  this.setCat = function(clickedCat) {
    self.currentCat(clickedCat)
  };
  // When clicked on something and function runs, object that was clicked on will be passed to function.
}
```

- Make cats show up  in listen
- Make current cat change when clicked

```
<ul data-bind="foreach: catList">
  <li data-bind="text: name, click: $parent.setCat"></li>
</ul>
```

## Backbone JS

- Organizational library
- Separation of concerns
- Model, view, presenter (MVP)
  - Some consider it as MV*
- [Documentation](http://backbonejs.org)

## Getting Started With APIs

- Example Google Maps
- [Google Developer Console](https://console.developers.google.com)
- Choose APIs
- Create credentials, select API key
- Full code described below on [GitHub](https://github.com/udacity/ud864)

### Google Maps API

```
<body>
  <div id="map"></div>
  <script>
    var map;
    function initMap() {
      // Constructor creates new map, only center and zoom required.
      map = new google.maps.Map(document.getElementById('map'), {
        center: {lat: 40.7413549, lng: -73.9980244},
        zoom: 13
      });
      var tribeca = {lat: 40.719526, lng: -74.0089934};
      var marker = new google.maps.Marker({
        position: tribeca,
        map: map,
        title: 'First Marker!'
      });
      var infowindow = new google.maps.InfoWindow({
        content: 'Sample info window text'
      });
      marker.addListener('click', function() {
        infowindow.open(map, marker);
      });
  </script>
  <script async defer
      src="https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&v=3&callback=initMap">
  </script>
</body>
```

- Insert API key
- Loads JavaScript API asynchronously
- Zoom level goes up to 21
- `var tribeca` is sample point where marker is set on map
- `var marker` creates new marker instance at position `tribeca`, on `map` with specified movie_title
- `var infowindow` creates information window instance to be displayed above marker
  - `marker.addListener` is event listener so that info window only opens when marker is clicked, passing in map on which to open and marker at which to anchor
- [Google Maps JavaScript API V3 Reference](https://developers.google.com/maps/documentation/javascript/reference)

### Showing Multiple Locations

```
<body>
  <div id="map"></div>
  <script>
    var map;
    // Create new blank array for all listing markers.
    var markers = [];
    function initMap() {
      // Constructor creates new map, only center and zoom are required.
      map = new google.maps.Map(document.getElementById('map'), {
        center: {lat: 40.7413549, lng: -73.9980244},
        zoom: 13
      });
      var locations = [
        {title: 'Park Ave Penthouse', location: {lat: 40.7713024, lng: -73.9632393}},
        {title: 'Chelsea Loft', location: {lat: 40.7444883, lng: -73.9949465}},
        {title: 'Union Square Open Floor Plan', location: {lat: 40.7347062, lng: -73.9895759}},
        {title: 'East Village Hip Studio', location: {lat: 40.7281777, lng: -73.984377}},
        {title: 'TriBeCa Artsy Bachelor Pad', location: {lat: 40.7195264, lng: -74.0089934}},
        {title: 'Chinatown Homey Space', location: {lat: 40.7180628, lng: -73.9961237}}
      ];
      var largeInfowindow = new google.maps.InfoWindow();
      var bounds = new google.maps.LatLngBounds();
      // Following group uses location array to create array of markers on initialize.
      for (var i = 0; i < locations.length; i++) {
        // Get position from location array.
        var position = locations[i].location;
        var title = locations[i].title;
        // Create marker per location, and put into markers array.
        var marker = new google.maps.Marker({
          map: map,
          position: position,
          title: title,
          animation: google.maps.Animation.DROP,
          id: i
        });
        // Push marker to our array of markers.
        markers.push(marker);
        // Create onclick event to open infowindow at each marker.
        marker.addListener('click', function() {
          populateInfoWindow(this, largeInfowindow);
        });
        bounds.extend(markers[i].position);
      }
      // Extend boundaries of map for each marker.
      map.fitBounds(bounds);
    }
    function populateInfoWindow(marker, infowindow) {
      // Check to make sure infowindow is not already opened on this marker.
      if (infowindow.marker != marker) {
        infowindow.marker = marker;
        infowindow.setContent('<div>' + marker.title + '</div>');
        infowindow.open(map, marker);
        // Make sure marker property is cleared if infowindow is closed.
        infowindow.addListener('closeclick',function(){
          infowindow.setMarker = null;
        });
      }
    }
  </script>

  <script async defer
      src="https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&v=3&callback=initMap">
  </script>

</body>
```

- Array containing locations with latitudes and longitudes
- Loop through locations and create one marker per location
- Keep created markers in array
- Info window reflects respective marker's information with on-click event on each marker
  - `this` is marker that has been clicked
  - `largeInfowindow` was created and initialized in stop
  - `function populateInfoWindow` that opens info window
- `function populateInfoWindow` sets content to `marker.title` and opens window on marker
- `var bounds` adjust boundaries of visible map so that all markers fit on screen
  - Captures southwest and northeast corner of viewpoint
  - `bounds.extend` extends boundaries for every marker made
- [Google Maps API Marker Documentation](https://developers.google.com/maps/documentation/javascript/markers)
- [Google Maps API Info Windows Documentation](https://developers.google.com/maps/documentation/javascript/infowindows)
- [Google Maps API Info Data Layer Documentation](https://developers.google.com/maps/documentation/javascript/datalayer)
- [Google Maps API Info Fusion Tables Layer Documentation](https://developers.google.com/maps/documentation/javascript/fusiontableslayer)

```
<body>
  <div class="container">
    <div class="options-box">
      <h1>Find Your New NYC Home</h1>
      <div>
        <input id="show-listings" type="button" value="Show Listings">
        <input id="hide-listings" type="button" value="Hide Listings">
      </div>
    </div>
    <div id="map"></div>
  </div>
  <script>
    var map;
    // Create new blank array for all listing markers.
    var markers = [];
    function initMap() {
      // Constructor creates new map, only center and zoom are required.
      map = new google.maps.Map(document.getElementById('map'), {
        center: {lat: 40.7413549, lng: -73.9980244},
        zoom: 13,
        mapTypeControl: false
      });
      var locations = [
        {title: 'Park Ave Penthouse', location: {lat: 40.7713024, lng: -73.9632393}},
        {title: 'Chelsea Loft', location: {lat: 40.7444883, lng: -73.9949465}},
        {title: 'Union Square Open Floor Plan', location: {lat: 40.7347062, lng: -73.9895759}},
        {title: 'East Village Hip Studio', location: {lat: 40.7281777, lng: -73.984377}},
        {title: 'TriBeCa Artsy Bachelor Pad', location: {lat: 40.7195264, lng: -74.0089934}},
        {title: 'Chinatown Homey Space', location: {lat: 40.7180628, lng: -73.9961237}}
      ];
      var largeInfowindow = new google.maps.InfoWindow();
      // Following group uses location array to create array of markers on initialize.
      for (var i = 0; i < locations.length; i++) {
        // Get position from location array.
        var position = locations[i].location;
        var title = locations[i].title;
        // Create marker per location, and put into markers array.
         var marker = new google.maps.Marker({
          position: position,
          title: title,
          animation: google.maps.Animation.DROP,
          id: i
        });
        // Push marker to our array of markers.
        markers.push(marker);
        // Create onclick event to open infowindow at each marker.
        marker.addListener('click', function() {
          populateInfoWindow(this, largeInfowindow);
        });
      }
      document.getElementById('show-listings').addEventListener('click', showListings);
      document.getElementById('hide-listings').addEventListener('click', hideListings);
    }
    function populateInfoWindow(marker, infowindow) {
      // Check to make sure infowindow is not already opened on this marker.
      if (infowindow.marker != marker) {
        infowindow.marker = marker;
        infowindow.setContent('<div>' + marker.title + '</div>');
        infowindow.open(map, marker);
        // Make sure marker property is cleared if infowindow is closed.
        infowindow.addListener('closeclick', function() {
          infowindow.marker = null;
        });
      }
    }
    // This function will loop through markers array and display them all.
    function showListings() {
      var bounds = new google.maps.LatLngBounds();
      // Extend boundaries of map for each marker and display marker
      for (var i = 0; i < markers.length; i++) {
        markers[i].setMap(map);
        bounds.extend(markers[i].position);
      }
      map.fitBounds(bounds);
    }
    // This function will loop through listings and hide them all.
    function hideListings() {
      for (var i = 0; i < markers.length; i++) {
        markers[i].setMap(null);
      }
    }
  </script>

  <script async defer
      src=
      "https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&v=3&callback=initMap">
  </script>

</body>
```

- Added buttons to hide and show locations
- `document.getElementById().addEventListener()` is event listener that trigger respective function

### Applying Styling

```
<body>
    <div class="container">
      <div class="options-box">
        <h1>Find Your New NYC Home</h1>
        <div>
          <input id="show-listings" type="button" value="Show Listings">
          <input id="hide-listings" type="button" value="Hide Listings">
        </div>
      </div>
      <div id="map"></div>
    </div>
    <script>
      var map;
      // Create new blank array for all listing markers.
      var markers = [];
      function initMap() {
        // Create styles array to use with map.
        var styles = [
          {
            featureType: 'water',
            stylers: [
              { color: '#19a0d8' }
            ]
          },{
            featureType: 'administrative',
            elementType: 'labels.text.stroke',
            stylers: [
              { color: '#ffffff' },
              { weight: 6 }
            ]
          }
        ];
        // Constructor creates new map, only center and zoom are required.
        map = new google.maps.Map(document.getElementById('map'), {
          center: {lat: 40.7413549, lng: -73.9980244},
          zoom: 13,
          styles: styles,
          mapTypeControl: false
        });
        var locations = [
          {title: 'Park Ave Penthouse', location: {lat: 40.7713024, lng: -73.9632393}},
          {title: 'Chelsea Loft', location: {lat: 40.7444883, lng: -73.9949465}},
          {title: 'Union Square Open Floor Plan', location: {lat: 40.7347062, lng: -73.9895759}},
          {title: 'East Village Hip Studio', location: {lat: 40.7281777, lng: -73.984377}},
          {title: 'TriBeCa Artsy Bachelor Pad', location: {lat: 40.7195264, lng: -74.0089934}},
          {title: 'Chinatown Homey Space', location: {lat: 40.7180628, lng: -73.9961237}}
        ];
        var largeInfowindow = new google.maps.InfoWindow();
        // Style markers bit. This will be our listing marker icon.
        var defaultIcon = makeMarkerIcon('0091ff');
        var highlightedIcon = makeMarkerIcon('FFFF24');
        var largeInfowindow = new google.maps.InfoWindow();
        // Following group uses location array to create array of markers on initialize.
        for (var i = 0; i < locations.length; i++) {
          // Get position from location array.
          var position = locations[i].location;
          var title = locations[i].title;
          // Create marker per location, and put into markers array.
          var marker = new google.maps.Marker({
            position: position,
            title: title,
            animation: google.maps.Animation.DROP,
            icon: defaultIcon,
            id: i
          });
          // Push marker to our array of markers.
          markers.push(marker);
          // Create onclick event to open large infowindow at each marker.
          marker.addListener('click', function() {
            populateInfoWindow(this, largeInfowindow);
          });
          marker.addListener('mouseover', function() {
            this.setIcon(highlightedIcon);
          });
          marker.addListener('mouseout', function() {
            this.setIcon(defaultIcon);
          });
        }
        document.getElementById('show-listings').addEventListener('click', showListings);
        document.getElementById('hide-listings').addEventListener('click', hideListings);
      }
      function populateInfoWindow(marker, infowindow) {
        // Check to make sure infowindow is not already opened on this marker.
        if (infowindow.marker != marker) {
          infowindow.marker = marker;
          infowindow.setContent('<div>' + marker.title + '</div>');
          infowindow.open(map, marker);
          // Make sure marker property is cleared if infowindow is closed.
          infowindow.addListener('closeclick', function() {
            infowindow.marker = null;
          });
        }
      }
      // This function will loop through markers array and display them all.
      function showListings() {
        var bounds = new google.maps.LatLngBounds();
        // Extend boundaries of map for each marker and display marker
        for (var i = 0; i < markers.length; i++) {
          markers[i].setMap(map);
          bounds.extend(markers[i].position);
        }
        map.fitBounds(bounds);
      }
      // This function will loop through listings and hide them all.
      function hideListings() {
        for (var i = 0; i < markers.length; i++) {
          markers[i].setMap(null);
        }
      }
      // Icon is 21 px wide by 34 high, origin of 0, 0 and anchored at 10, 34.
      function makeMarkerIcon(markerColor) {
        var markerImage = new google.maps.MarkerImage(
          'http://chart.googleapis.com/chart?chst=d_map_spin&chld=1.15|0|'+ markerColor +
          '|40|_|%E2%80%A2',
          new google.maps.Size(21, 34),
          new google.maps.Point(0, 0),
          new google.maps.Point(10, 34),
          new google.maps.Size(21,34));
        return markerImage;
      }
    </script>

    <script async defer
        src=
        "https://maps.googleapis.com/maps/api/js?key=MYAPIKEY&v=3&callback=initMap">
    </script>

  </body>
```

- `styles: styles` sets own styles to Maps
  - Cascading and if no value is provided default applies
- `mapTypeControl: false` disables ability for user to change map type
- `var defaultIcon` sets default color of markers by creating makeMarkerIcon object
- `var highlightedIcon` sets color of marker on hoverb y creating makeMarkerIcon object
- `function makeMarkerIcon()` takes in `markerColor` and creates new `var markerImage`
- `icon: defaultIcon` sets default icon to marker
- `marker.addListener()` is event listener for hover
- [Start Styling your Map](https://developers.google.com/maps/documentation/javascript/styling)
- Pre-built map styles: [Snazzy Maps](https://snazzymaps.com)

### Static Maps And Street View Images

- Set pitch and heading to determine camera angle
- [GitHub Udacity](https://github.com/udacity/ud864/blob/master/Project_Code_6_StaticMapsAndStreetViewImagery.html)

### Drawing

- [GitHub Udacity](https://github.com/udacity/ud864/blob/master/Project_Code_7_Drawing.html)

### Geocoding

- Getting address from specific location
- [GitHub Udacity](https://github.com/udacity/ud864/blob/master/Project_Code_8_GeocodingInTheApp.html)
- [Google Maps Geocoding API](https://developers.google.com/maps/documentation/geocoding/intro)

### Elevation

- [Google Maps Elevation API](https://developers.google.com/maps/documentation/elevation/intro)
- [Google Maps Elevation Serice](https://developers.google.com/maps/documentation/javascript/elevation)

### Distance Matrix

- [Google Maps Distance Matrix API](https://developers.google.com/maps/documentation/distance-matrix/)
- [GitHub Udacity](https://github.com/udacity/ud864/blob/master/Project_Code_9_MyCommuteDistanceMatrixAPIPart2.html)

### Directions

- [Google Maps Directions API](https://developers.google.com/maps/documentation/directions/)

### Places

- Find addresses, establishments or business at specific location

### Geolocation

- Service to get location information from cell towers, wifi nodes when GPS is weak or not available
- Returns location and accuracy measure
- [GitHub Udacity](https://github.com/udacity/ud864)

### Additional

- Use developer console to see quota of used API Requests
- Whitelist domains to limit which ones are able to use API key
- Kinds of restrictions
  - Queries per day (QPD)
  - Queries per second (QPS)
- [Google Maps API Pricing And Plans](https://developers.google.com/maps/pricing-and-plans/)
- [Google Developers YouTube Channel](https://www.youtube.com/user/GoogleDevelopers/featured)

## Resources

- [AJAX Request Documentation](http://api.jquery.com/jquery.ajax/)
- [Largest API Directory Online](https://www.programmableweb.com/apis/directory)
- [Google APIs](https://developers.google.com/apis-explorer/#p/)
- [New York Times API](http://developer.nytimes.com/)
- Article search API that pull article from 1851 until today
- Requires API key
- [Wikipedia API](https://www.mediawiki.org/wiki/API:Main_page)
- [Simple Knockout JS example](http://jsfiddle.net/rniemeyer/3Lqsx/)
- [TodoMVC](http://todomvc.com) Todo application build in variety of frameworks
- [Simple HTTP Server with Python](http://www.linuxjournal.com/content/tech-tip-really-simple-http-server-python)

# Deploying To Linux Servers

## Intro To linux

- 80% of public internet services run on Linux
- Free for use, hundreds of versions available
- Many distributions available e.g. Ubuntu (for server, desktop and mobile phone, consistent updates), Fedora, CentOS, Redhat (popular for enterprises, paid license), ArchLinux, CoreOS, Mandriva, Linux Mint, Debian (parent distribution of Ubunto, very reliable, few updates), Suse
- Source for Linux distributions: [DistroWatch](https://distrowatch.com)

## Getting Started With Vagrant

- Download and install [VirtualBox](https://www.virtualbox.org/wiki/Download_Old_Builds_5_1)
  - Make sure that version supports Vagrant
- Download and install [Vagrant](https://www.vagrantup.com)
- Create new folder and open in terminals
- `vagrant init ubuntu/trusty64` to select virtual machine to run
- `vagrant up` to download and start running virtual machine
- Prompt `vagrant@vagrant-ubuntu-trusty-64:` confirms that inside Linux box
- Automatically in home directory when logged in
  - `/home` is root level, highest level
- `ls` in home directory shows users
- `ls -a` shows all files including hidden ones
- `ls -al` added `l` flag will list results in long and detailed format
- If first character starts with "d" its directory, if it starts with "-" its file
- Go to top level root folder with `cd /`
- `ls -al` to see content in root directory
  - `/etc` contains configuration files
  - `/var` for variable files which are expected to change in size over time e.g. system and application logs
  - `/bin` contains executable binary files accessible by all users, files required for boot up and system maintenance purposes
  - `/sbin` contains binary files only accessible by root user
  - `/lib` for libraries
  - `/usr` for user programs, files not required for boot up and system maintenance

### Vagrant Commands

- `vagrant status` shows current status of virtual machine, should return "default running(virtualbox)"
- `vagrant suspend` suspends virtual machine, is put into sleep mode and machine state is saved, for quick breaks if machine should not be running in meantime
- `vagrant up` get virtual machine up and running again, no redownload needed
- `vagrant ssh` connects to and logs into virtual machine, shows performance statistics
- `vagrant halt` turns power off and frees up all RAM used, works is saved, used for extensive breaks
- `vagrant destroy` destroys virtual machine, work is not saved

### Understanding $PATH

- Shortcut system within $PATH variable
- `echo $PATH` returns directories that Linux will progress through looking for binary if user types name like `ls`
  - Checks each directory for executable file for `ls`

## Linux Security

- Rule of least privilege: User or application only has enough permissions to do its job
- Super user is root and its often disabled to log in as root remotely
- `sudo` prefix allows to run following command as if user was root, to run administrative commands
  - In this case user can run administrative commands while being logged in remotely but not as root, attacker can not log in as root remotely and does not know username of sudo eligible user
- `cat /etc/apt/sources.list` to see available package sources
- Updating available package source list with `sudo apt-get update`
  - Checks which software is available, does not change software itself
- Upgrading installed packages with `sudo apt-get upgrade`
  - Review list and test in non-production environment if upgrading production server
- `man apt-get` shows everything that `apt-get` can do
- `sudo apt-get autoremove` removes packages that are no longer required
- `sudo apt-get install finger` to install application `finger`

### Using Finger

- Will look up information about user
- `finger` will return output about users that are currently logged in
- `finger vagrant` returns additional information about user `vagrant`
- `cat /etc/passwd` stores information about each user, each entry is single user, entries separated by colons
  - Includes user ID and group ID, root user has 0 as user ID and group ID
  - Last two fields are home directory and default shell

### User Management

- `sudo adduser john` to add new user called `john`
  - New password requested, password can not be seen
  - Additional information can be entered, optional
  - `finger john` to confirm that user is created
- Connect as new users
  - Open new terminal on local machine
  - Connect to server by running `ssh john@127.0.0.1 -p 2222`
    - `ssh` is application used to remotely connect to server
    - `127.0.0.1` is IP address to connect to
    - `john` is username
    - `-p 2222` connects to port 2222 which was automatically set up
  - Confirm with yes and enter password
- Giving user permission to use `sudo` command
  - Log in as `vagrant` or user that can perform administrative tasks
  - Run `sudo cat /etc/sudoers`
  - Lists all users that can use `sudo` command and groups
    - Groups start with "%"
  - Customizations are kept in separate directory `/etc/sudoers.d` so that system updates can not erase modifications
  - Run `sudo ls /etc/sudoers.d` to see users with permission
  - Adding new user to `sudo` permissions listen
    - Copy vagrant file and rename it by `sudo cp /etc/sudoers.d/vagrant /etc/sudoers.d/john`
    - Edit file with `sudo nano /etc/sudoers.d/john`
    - Change name "vagrant" to "john" in GNU nano
    - Save file
  - Switch to new user "john" and run any `sudo` command
- Force user's password to expire by `sudo passwd -e john`
  - User needs to reset password next time they log in

### Alternative Authentication Methods

- Key based authentication is based on files stored on server and personal machine from which to log in
  - Used to authenticate client and server
  - Server sends random message to client, client encrypts message with private key, sends encrypted message back to server, server decrypts message with public key, if message is same message as send originally, then client is authenticated
- Generate key pair on local machine, not on server
  - Generate pair with `ssh-keygen`
  - Enter filename for key pair e.g. `/Users/Folder/.ssh/linuxCourse`
    - `/.ssh/` is default directory that key pair should exist in
  - Enter passphrase that prevents users from using key pair file
  - Two files are generated: `linuxCourse` and `linuxCourse.pub`, latter will be stored on server to allow key based authentication
  - Per default, `ssh-keygen` generates RSA keys, also supports DSA, ECDSA, ED25519
    - SHA256 is hashing algorithm that is not supported for public key encryption
- Put public key on server
  - Log in to server
  - `mkdir .ssh` to create new directory, default directory for keys
  - `touch .ssh/authorized_keys` to create new file that stores all public keys that account is allowed to use for authentification
  - One key per line in file
  - Read out content of `linuxCourse.pub` on local machine and copy it with right click
  - On servers as user, edit key file with `nano .ssh/authorized_keys`, paste public key and save it
- Add security features to that other users can not gain access to account
  - Run `chmod 700 .ssh`
  - Run `chmod 644 .ssh/authorized_keys`
- Finally, log in as user with key based authentication by running `ssh john@127.0.0.1 -p 2222 -i -/.ssh/linuxCourse`
  - Enter passphrase for local key pair file
  - Logged in to server without entering remote password
- Disable password based logins
  - Users are only able to login using keypair
  - `sudo nano /etc/ssh/sshd_config` to edit configuration file
  - Look for `PasswordAuthentification yes` line and change to `no`
  -  Restart service so that it runs with new configuration file and changes are implemented
    - Run `sudo service ssh restart`
  - No user is allowed to log in with username and password any longer

### File Permissions

- View home directoy with `ls -al` as example
- Each file has three entries
- For example `rw-r--r--`
- Three entries with three characters each, for example `rw-` `r--` `r--`
- Are labeled owner, group, everyone respectively
- In this case owner has `rw-` which means he can read and write file but can not execute it
- Users within group and everyone have `r--` which means they can read but not write or execute file
- `rwx` would allow to read, write and execute file
- Second and third columns in `ls -al` output are owner and group for respective entry
  - Group with name equivalent to username is automatically created for each user created
  - Group named as user
-  Octal permissions
  - Values are translated: `r` = 4, `w` = 2, `x` = 1, no permissions = 0
  - To give read and execute access: `r` = 4, `x` = 1 which is 5 in sum
  - Give number to individual user, group and everyone
  - Foe example converting `rw-r--r--` to octal form would result in 644
- Change file permissons with `chmod 644 .ssh/authorized_keys`
- Change file group with `sudo chgrp john .bash_history`
- Change file owner with `sudeo chown john .bash_history`

### Ports

- Ports used so that server knows which application can handle each kind of request
- Each application is specified to respond to request destined for specific port
  - For example, web server would respond to request on port 80 which is default for HTTP
- Only listen on ports that are required for application to run
- One can set ports that server is allowed to accept requests from using firewall

#### Common Ports

- HTTP on port 80
- HTTPS on port 744
- SSH on port 22
- FTP on port 21
- POP3 on port 110
- SMTP on port 25

### Firewall Setup

- Ubunto comes with firewall preinstalled called "ufw"
- `sudo ufw status` to check status
- Add rules and configure firewall without turning it on yet
  - `sudo ufw default deny incoming` to initially block all incoming requests
    - Thereby also incoming SSH connections are blocked, turning on firewall with this setting would make server inaccessible, hence, setup firewall early on in development process
  - `sudo ufw default allow outgoing` to allow all outgoing connections and requests servers sends out to internet
  - Only allow needed incoming requests by configuring ports
  - `sudo ufw allow ssh` to allow ssh connections
  - `sudo ufw allow 2222/top` to allow ssh connections if servers is run locally with vagrant, otherwise this can be ignored
  - `sudo ufw allow www` to allow basic HTTP requests
  - `sudo ufw show added` to check added ports
- `sudo ufw enable` to enable firewall
- Confirm that all rules are set up as indicated by running `sudo ufw status`
- Returns all rules and that firewall is active

## Web Application Servers

- Use Apache HTTP Server to respond to HTTP requests
- Configure Apache to hand-off specific requests to Python to allow dynamic websites
- Setup PostgreSQL to allow data-driven websites

### Vagrant Prerequisites

- Change in configuration so that port 8080 gets forwarded from host machine to guest machine meaning vagrant virtuale environment

### Installing Apache

- Use Apache HTTP server to respond to HTTP requests
- Mosts commonly installed web server on internet
- `sudo apt-get install apache2` to install Apache with package manager
- Visit localhost on port 8080 in browser to confirm Apache is working if it returns default page
- By default Apache serves files from `/var/www/html` directory which contains `index.html` file

### Installing WSGI Module

- Apache can be configured to hand-off certain requests to application handler mog_wsgi
- `sudo apt-get install libapache2-mod-wsgi` to install
- Edit `/etc/apache2/sites-enabled/000-default.conf` file to configure Apache to handle requests using WSGI module
  - File shows how to handle requests and where to find files for particular site
  - More information: [Apache Documentation](https://httpd.apache.org/docs/2.2/configuring.html)
- Restart Apache with `sudo apache2ctl restart`

### First WSGI Application

- Most Python web frameworks are WSGI compliant including Flask and Django
- `/var/www/html/myapp.wsgi` is Python application besides having `.wsgi` extension

### Installing PostgreSQL

- Install PostgreSQL with `sudo apt-get install postgresql`
- Since web server and database server are on same machine, there is no need to modify firewall settings
  - Both communicate internally

## Resources

- Bash startup files: [GNU](http://www.gnu.org/software/bash/manual/html_node/Bash-Startup-Files.html)
- Add directory to $PATH: [Ask Ubuntu](https://askubuntu.com/questions/60218/how-to-add-a-directory-to-the-path)
- [Ubuntu Packages](https://packages.ubuntu.com)
- [Apache HTTP Server](http://httpd.apache.org)
- SSH and how to access remote server and edit files: [Udacity Webcast](https://www.youtube.com/watch?v=HcwK8IWc-a8)
- Intro to TMux: [Udacity Webcast](https://www.youtube.com/watch?v=hZ0cUWWixqU)
- Deploying Flask App with Heroku: [Udacity Webcast](https://www.youtube.com/watch?v=5UNAy4GzQ5E)
