## My Ruby Environment

#### John Fearnside
#### jfearnside@avvo.com

---

## Goals
- Disposable
- Up-to-date
- Isolated
- Maintainable

---

## macOS
- iTerm2
- Xcode
- Docker

---

## Homebrew

https://brew.sh/
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

---

## Functions, part 1: brew
```
bod() { brew update && brew outdated && brew doctor; }
buc() { brew upgrade; brew cleanup; }
```

---

## Bash
- instead of _system_ Bash:
```
brew install bash
```

---

## `rbenv` & friends
```
brew install rbenv
```
- update profile files as per instructions
- start a new terminal session, then verify `rbenv -v`
```
brew install ruby-build
mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/rbenv-each.git "$(rbenv root)"/plugins/rbenv-each
```
- start a new terminal session, then verify `ruby-build --version`

---

## Functions, part 2: rbenv
- Bash functions in `~/.bashrc`
- Prefer functions, not aliases
- information about rubies
- add/remove rubies

```
rbs() { rbenv -v; ruby-build --version; rbenv versions; echo "CURRENT RUBY: $(ruby -v)"; }
rbis() { ruby-build --definitions | column; }
rb+() { rbenv install "$1"; }
rb-() { rbenv uninstall "$1"; }
```
---

## Install Rubies
```
rbis
rb+ 2.4.1
rb+ 2.3.4
rb+ jruby-9.1.8.0
```

---

## Functions, part 3: switching Rubies
```
rb0() { rbenv local system; rbs; }
rb2() { rbenv local 2.4.1; rbs; }
rbj() { rbenv local jruby-9.1.8.0; rbs; }
rb234() { rbenv local 2.3.4; rbs; }
```

---

```
rgs() { rbenv each -v gem list; }
rg+() { rbenv each -v gem install "$@"; }
rg-() { rbenv each -v gem uninstall "$@"; }
rgo() { rbenv each -v gem outdated; }
rgu() { rbenv each -v gem update "$@"; }
rgc() { rbenv each -v gem cleanup; }
```

## Bundler

---

## Functions, part 3

---

## Functions, part 4: advanced

rbup_() {
  brew upgrade rbenv 2> /dev/null
  brew upgrade ruby-build 2> /dev/null
  rbenv -v
  ruby-build --version
}
rbis_() { ruby-build --definitions; }
rbis() { rbis_ | column; }
rbup() { rbis_ > rbis0.txt; rbup_; rbis_ > rbis1.txt; gdiff rbis0.txt rbis1.txt; }


## Q & A

---

## Resources
https://gitpitch.com/jwfearn/slides-my-rbenv/
https://brew.sh/
https://github.com/rbenv/rbenv/
https://github.com/rbenv/rbenv-each/

<!--
TODO: screenshots from BS and SF to show what data moves where

Intro - Chris
Batch - Gowthami
Realtime - John
Leveraging - Elisabeth
Execution - Chris

-->