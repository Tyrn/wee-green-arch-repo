# wee-green-arch-repo

_An Arch Linux unofficial repository, my very own_

Make sure that the project has its own GitHub Page, like
`myname.github.io/wee-green-arch-repo`, otherwise you'll run into
trouble with the symlinks like `x86_64/wee-green-arch-repo.db`.

It's possible to work with the package source anywhere on the file system;
for now we confine ourselves to the `src/` directory alongside this
BUILDME file (see `.gitignore`).

- If you're working with an entirely new project, create the database in
  _architecture_ directory. **Skip this entry if the repository project
  already exists**.

```
mkdir x86_64
cd x86_64
repo-add wee-green-arch-repo.db.tar.gz
```

Assuming we want to build the `pulseview-git` AUR package and
put it into `wee-green-arch-repo`:

- Fetch the sources

```
mkdir src
cd src
```

`src/` directory must be empty, and located at the root of the project.

```
aur fetch -r pulseview-git
```

- Create a list of sources to be built (the package and its dependencies)

```
ls -d */ | sed 's|/$|/|' > _pkglist.txt
```

- Build all

```
aur build -a ./_pkglist.txt -d "wee-green-arch-repo" -r "$(dirname $(pwd))/x86_64" --margs -s
```

- Add the build artifacts to the Git repository, commit and push
