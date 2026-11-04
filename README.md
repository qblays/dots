Config files for various programs, managed with GNU Stow.

This repo uses `--no-folding` in `.stowrc`. Stow creates real directories in
`$HOME` and symlinks individual config files into them, instead of symlinking
whole config directories. That keeps application-generated state files out of
the Git working tree.

Install or refresh packages from the repo root:

```sh
stow -R alacritty kanata doom mpv neovim tmux vifm zsh
```

Install or update external runtime repositories:

```sh
./scripts/sync-external
```

External repositories such as TPM, Zinit, and Vifm colors are normal Git
checkouts under `$HOME`, not submodules of this repo. Add new managed externals
to `scripts/sync-external`, not to `.gitmodules`.

Add new config files directly under the matching package directory, then restow
that package:

```sh
stow -R neovim
git add neovim/.config/nvim/path/to/file.lua
```

Do not add generated files such as lock files, editor swap files, generated zsh
completions, Vifm state, or plugin install directories. Those should stay in
`$HOME` and are ignored if they accidentally appear in the repo.


## Keyboard remapping (kanata)

`kanata` runs as the root system service from its package, which reads
`/etc/kanata.kbd`. Link the config there once:

```sh
stow -R kanata
sudo ln -s ~/.config/kanata/kanata.kbd /etc/kanata.kbd
sudo systemctl enable --now kanata
```

After editing the config:

```sh
kanata --cfg ~/.config/kanata/kanata.kbd --check
sudo systemctl restart kanata
```

# TO add:
git, lazygit, plugins for yazi
