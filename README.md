# yarn-completion

This plugin is a fork of [zsh-better-npm-completion](https://github.com/lukechilds/zsh-better-npm-completion). It works the same way, as you can see with `npm` demo:

<img src="demo.gif" width="690">

* Makes `yarn add` recommendations from npm cache
* Makes `yarn remove` recommendations from `dependencies`/`devDependencies`
* Shows detailed information on script contents for `yarn run`
* Falls back to default yarn completions if we don't have anything better

## Installation

### Using [Antigen](https://github.com/zsh-users/antigen)

Bundle `zsh-better-npm-completion` in your `.zshrc`

```shell
antigen bundle buonomo/yarn-completion
```

### Using [zplug](https://github.com/b4b4r07/zplug)
Load `zsh-better-npm-completion` as a plugin in your `.zshrc`

```shell
zplug "buonomo/yarn-completion", defer:2

```
### Using [zgen](https://github.com/tarjoilija/zgen)

Include the load command in your `.zshrc`

```shell
zgen load buonomo/yarn-completion
```

### As an [Oh My ZSH!](https://github.com/robbyrussell/oh-my-zsh) custom plugin

Clone `yarn-completion` into your custom plugins repo

```shell
git clone https://github.com/buonomo/yarn-completion ~/.oh-my-zsh/custom/plugins/yarn-completion
```
Then load as a plugin in your `.zshrc`

```shell
plugins+=(yarn-completion)
```

### Manually
Clone this repository somewhere (`~/.yarn-completion` for example)

```shell
git clone https://github.com/buonomo/yarn-completion.git ~/.yarn-completion
```
Then source it in your `.zshrc`

```shell
source ~/.yarn-completion/yarn-completion.plugin.zsh
```

## Module Install Cache

When running `yarn add rea<tab>`, it will perform an `npm search` for matching packages. In addition
it will look in your local npm cache directory for package suggestions. However building this list
can be pretty slow. This completion makes use of the zsh completion caching mechanism to cache the
module list if you have caching enabled. 

We try to enable it by default, however if you have something
like below in your zshrc forces cache for all completions to be turned off.

```zsh
zstyle ':completion:*' use-cache off
```

To specifically turn npm cache back on, you may add the following:

```zsh
zstyle ':completion::complete:npm::' use-cache on
```

By default the cache will be valid for 1 hour. But can be modified by setting a cache policy like this:

```zsh
_yc_add_cache_policy() {
  # rebuild if cache is more than 24 hours old
  local -a oldp
  # See http://zsh.sourceforge.net/Doc/Release/Expansion.html#Glob-Qualifiers
  # Nmh+24 ... N == NULL_GLOB, m == modified time, h == hour, +24 == +24 units (i.e. [M]onth, [w]weeks, [h]ours, [m]inutes, [s]econds)
  oldp=( "$1"(Nmh+24) )
  (( $#oldp ))
}
zstyle ':completion::complete:npm::' cache-policy _yc_add_cache_policy
```


## Related

- [`zsh-nvm`](https://github.com/lukechilds/zsh-nvm) - Zsh plugin for installing, updating and loading `nvm`
- [`gifgen`](https://github.com/lukechilds/gifgen) - Simple high quality GIF encoding 

## License

MIT © Ulysse Buonomo
