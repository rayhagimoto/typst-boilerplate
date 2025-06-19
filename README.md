# Typst project template

This directory defines a project structure for typst notes, including vscode settings.

The vscode settings are irrelevant if you're not using vscode. However, if you're using vscode the [.vscode/settings.json](.vscode/settings.json) assumes [Trigger Task on Save](https://open-vsx.org/extension/Gruntfuggly/triggertaskonsave) by [Gruntfuggly](https://open-vsx.org/namespace/Gruntfuggly) is installed. 
At the time of writing I'm using v0.2.18.

# Quick start

I keep my typst notes in `$HOME/typst` so I clone this repo using `git clone https://github.com/rayhagimoto/typst-project $HOME/typst/$PROJECT_NAME`.

The build script in [`scripts/build.sh`](scripts/build.sh) assumes that `$PROJECT_NAME` is of the form `$TOPIC-notes`. Then it compiles `src/main.typ` to `$TOPIC.pdf`. For example, if I had `PROJECT_NAME=stochastic-calculus-notes` then the output filename would be `stochastic-calculus-notes.pdf`, in the project root.

# Template

I use a [template](https://github.com/rayhagimoto/typst-template), which I  installed by cloning the repo to `$HOME/.local/share/typst/packages/local/templates/1.0.0` 

```
~/.local/share/typst
└── packages
    └── local
        └── templates
            └── 1.0.0
                ├── lib.typ
                ├── problems.typ
                ├── template.typ
                ├── typst.toml
                └── utils.typ
```

The build script sets `$XDG_DATA_HOME=~/.local/share` since typst looks at `$XDG_DATA_HOME/typst/packages` for packages. 
They are then imported using `#import "@local/templates:1.0.0" : *`.

# Setting up the build environment for using my template
(Instructions accurate at time of writing June 19 2025)

Instructions on how to set up typst with my template on WSL2 Ubuntu-24.04.1 LTS.

Get the typst compiler from https://github.com/typst/typst. I followed the instructions there and ran `snap install typst` and got typst 0.13.1.

I install my template by doing

```
# Clone the repo into the directory where typst compiler can find it
git clone https://github.com/rayhagimoto/typst-template ~/.local/share/typst/packages/local/templates/1.0.0

# Install msft fonts (I'm only doing this for Arial, I should change to some other sans serif font...)
sudo apt-get update
sudo apt-get install msttcorefonts

# Install lmodern font
wget https://www.gust.org.pl/projects/e-foundry/latin-modern/download/lm2.004otf.zip && \
    mkdir -p /usr/share/fonts/lmodern && \
    unzip lm2.004otf.zip -d /usr/share/fonts/lmodern && \
    rm lm2.004otf.zip && \
    fc-cache -fv
```