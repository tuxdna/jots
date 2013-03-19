# Git notes

## Git SVN:
git stash
git svn fetch
git svn rebase
git stash pop

git rebase -i git-svn # use pick/squash properly and edit messages
git rebase -i --abort


## Understanding Git
<http://stackoverflow.com/questions/261557/what-do-i-need-to-read-to-understand-how-git-works>

<http://blog.shinetech.com/?p=150>

Git internals from the bottom-up: <http://newartisans.com/2008/04/git-from-the-bottom-up/>

Git for computer scientists: <http://eagain.net/articles/git-for-computer-scientists/>

Excellent video tutorial on how git actually works: <http://blip.tv/scott-chacon/git-talk-4113729>

Enlist the objects and their types:

    for k in `find .git/objects/ -type f  | cut -c14- | sed 's/\///'`; do echo -n "$k: "; git cat-file -t $k; done
    git hash-object
    git cat-file
    git ls-files
    git write-tree  # create a tree object from index
    git commit-tree #
    git update-ref
    git show-branch
    

MongoDB backend for git: <http://strangeowl.blogspot.com/2010/09/versioning-objects-and-mongodb.html>

    git gc
    git fsck --lost-found
    
Override .git directory location
    export GIT_DIR=/path/to/.git  OR GIT_DIR=/path/to/mygit :)
    

Git format patch

    git format-patch <revision> / HEAD
    git am # apply email patch
    git apply -R < N.patch



## Object Database: .git/

    content

    new_content = type + ' ' + content.size + '\0' + content
    sha = Digest::SHA1.hexdigest(new_content) ==> "e7ea61d5394b9b52dd0447281ab7df6eafbb1cd8"
    compressed = zlib::deflate(new_content)
    path = ".git/objects/e7/ea61d5394b9b52dd0447281ab7df6eafbb1cd8"
    
Git has two kind of object storage: packaged and loose
 * Above storage is loose storage.
 * Packed storage is created by git gc

## git gc

If these are all different versions of same file with only very minor changes:

    .git/objects/12/2086154c79bbe739e302034cfb745657aae0ce
    .git/objects/13/612471a6c0e685c206208ab4e683f6015c25ba
    .git/objects/b7/615e6e4426359359c611dd95e4fa47536895ce
    .git/objects/57/0200056879cdb7a75f0ec3fd101ea86ccde524
    
git gc will delta compress above versions and write into a pack file

    .git/objects/pack/ac/edc4e2aee731a806475bdcaadb80d9b4ec6409.pack
    .git/objects/pack/ac/edc4e2aee731a806475bdcaadb80d9b4ec6409.idx
    
And then remove all the other files versions


Types of git objects:

    blob: (type + ' ' + content.size + '\0' + content)

 * sha = Digest::SHA1::hexdigest
 * compressed = zlib::deflate

tree:

Working Directory

    ./                         .  tree: 1d345
     Makefile		   .  blob: dad65
     src/		      	   .  tree: h76f3
      a.c		      	   .  blob: 8de74
      b.c			   .  blob: 9h5fe
    
    tree [content size]\0
    
    mode   type  block-pointer  filename
    -----------------------------------
    040000 tree  1d345          ./
    100644 blob  dad65          Makefile
    040000 tree  h76f3          src/
    100644 blob  8de74          src/a.c
    100644 blob  9h5fe          src/b.c
    
    commit:
    
    commit [content size]\0
    tree 88f3223
    parent 1f6e09
    author Saleem Ansari <tuxdna@gmail.com> timestamp
    committer Saleem Ansari <tuxdna@gmail.com> timestamp
    this is a commit message
    
zlib::deflate(all of the above content)


tag:
	 
    tag [content size]\0
    object 7a8de3
    type commit
    tag v0.1.23
    tagger Saleem Ansari <tuxdna@gmail.com> timestamp
    this is tag for version 0.1
    

## Checkout in another folder

    git archive tag-name --prefix="tag-name/" | tar -xv

Exapmple

    mkdir /tmp/xyz
    git archive master | tar -x -C /tmp/xyz
