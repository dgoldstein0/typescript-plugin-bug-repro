# typescript-plugin-repro

This repo exists to show a bug in the combination of tsserver, typescript-plugin-css-modules, and typescript-plugin-yaml.  The latter is taken from https://github.com/rickdgeerling/typescript-plugin-yaml/tree/feat/support-ts-v5; as there is no published copy I could use, I had to copy the compiled outputs into this repo.

Basically, the bug: if you open index.ts in any typescript-supporting IDE - VSCode works, as does VIM with the tsuquyomi plugin - then one of the two imports won't resolve - corresponding to whichever plugin is currently specified first in tsconfig.json.

After a lot of logging in the two plugins and reading tsserver logs, my only real conclusion is that while typescript initializes both plugins, it just chooses not to use one of them.  My guess is that it's only using the last returned languageService - I've included my logging of the typescript-plugin-css-modules and it's pretty clear from the lack of those firing that after plugin initialization in tsserver, tsserver just doesn't use the plugin.
