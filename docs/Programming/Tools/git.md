# Git

## Local commands
### Basic commands
Initialize a repository
```bash
git init
```

Get the repository and files status
```bash
git status
```

Add or update files tracked by git
```bash
git add [--all | --update] {file name or path}
```

Remove files tracked by git (use the option to keep the file on disk)
```bash
git rm [--cached] {file name}
```

Commit changes to the working branch
```bash
git commit -m "{message}"
```

### Git history and rollback
Review commit history (see man for more options)
```bash
git log [--stat]
```

### Git branching
List or create a new branch
```bash
git branch [{name of the branch to create}]
```

Switch to another branch
```bash
git switch {name of the branch}
```



## Remote commands

