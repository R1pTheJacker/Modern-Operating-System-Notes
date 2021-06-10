## 1. Single-Level Directory Systems
- simple to locate files
- generally, only one user

### 1.2 Two-Level Directory Systems
- each user owns a private directory
- avoid conflicts among users

## 2. Hierarchical Directory Systems
- be able to create an arbitrary number of subdirectories 
- provide a powerful structuring tool for users

## 3. Path Names
To locate files, we need to use 'path'.

### 3.1 Absolute Path Name 
- start from root directory

### 3.2 Relative Path Name 
- '.' or '..'
- start from current working directory

## 4. Directory Operations
- Create 
>A directory is created. It is empty except for dot and dotdot, which are put there automatically by the system (or in a few cases, by the mkdir program).

- Delete 
>A directory is deleted. Only an empty directory can be delet ed. A directory containing only dot and dotdot is considered empty as these cannot be deleted.

- Opendir
>Directories can be read. For example, to list all the files in a directory, a listing program opens the directory to read out the names of all the files it contains. Before a directory can be read, it must be opened, analogous to opening and reading a file.

- Closedir
>When a directory has been read, it should be closed to free up internal table space.

- Readdir
>This call returns the next entry in an open directory. Formerly, it was possible to read directories using the usual read system call, but that approach has the disadvantage of forcing the programmer to know and deal with the internal structure of directories. In contrast, readdir always returns one entry in a standard format, no matter which of the possible directory structures is being used.

- Rename
>In many respects, directories are just like files and can be renamed the same way files can be.

- Link
>Linking is a technique that allows a file to appear in more than one directory. This system call specifies an existing file and a pathSEC. 4.2 DIRECTORIES 281 name, and creates a link from the existing file to the name specified by the path. In this way, the same file may appear in multiple directories. A link of this kind, which increments the counter in the file’s i-node (to keep track of the number of directory entries containing the file), is sometimes called a hard link.

- Unlink
>A directory entry is removed. If the file being unlinked is only present in one directory (the normal case), it is removed from the file system. If it is present in multiple directories, only the path name specified is removed. The others remain. In UNIX, the system call for deleting files (discussed earlier) is, in fact, unlink.