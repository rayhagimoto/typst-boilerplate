# Typst Project Template

This directory outlines a project structure for Typst notes, including VSCode settings.

If you're not using VSCode, the settings are irrelevant. However, if you are, the [.vscode/settings.json](.vscode/settings.json) file assumes that the [Trigger Task on Save](https://open-vsx.org/extension/Gruntfuggly/triggertaskonsave) extension by Gruntfuggly (v0.2.18 at the time of writing) is installed.

## Quick Start

I organize my Typst notes in `$HOME/typst`. To clone this repository, use the following command:

```bash
git clone https://github.com/rayhagimoto/typst-boilerplate $HOME/typst/$PROJECT_NAME
```

The build script located at [`scripts/build.sh`](scripts/build.sh) expects `$PROJECT_NAME` to follow the format `$TOPIC-notes`. It then compiles `src/main.typ` into `$TOPIC.pdf`. For instance, if `PROJECT_NAME` is `stochastic-calculus-notes`, the output filename will be `stochastic-calculus-notes.pdf` in the project root.

## Template Usage

I utilize a [template](https://github.com/rayhagimoto/typst-template), which I've installed by cloning the repository to `$HOME/.local/share/typst/packages/local/templates/1.0.0`. The directory structure is as follows:

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

The build script sets `$XDG_DATA_HOME=~/.local/share`, as Typst looks for packages in `$XDG_DATA_HOME/typst/packages`. These packages are then imported using:

```typst
#import "@local/templates:1.0.0" : *
```

## Setting Up the Build Environment for My Template

*(Instructions are accurate as of June 19, 2025)*

Here's how to set up Typst with my template on WSL2 Ubuntu-24.04.1 LTS:

1.  **Get the Typst Compiler:**
    Obtain the Typst compiler from [https://github.com/typst/typst](https://github.com/typst/typst). I followed the instructions there and installed it using `snap install typst`, which provided Typst 0.13.1.

2.  **Install My Template:**
    Clone the template repository into the directory where the Typst compiler can find it:

    ```bash
    git clone https://github.com/rayhagimoto/typst-template ~/.local/share/typst/packages/local/templates/1.0.0
    ```

3.  **Install Microsoft Fonts (Optional):**
    I primarily install these for Arial; consider an alternative sans-serif font if desired.

    ```bash
    sudo apt-get update
    sudo apt-get install msttcorefonts
    ```

4.  **Install Latin Modern Font:**

    ```bash
    wget https://www.gust.org.pl/projects/e-foundry/latin-modern/download/lm2.004otf.zip && \
        mkdir -p /usr/share/fonts/lmodern && \
        unzip lm2.004otf.zip -d /usr/share/fonts/lmodern && \
        rm lm2.004otf.zip && \
        fc-cache -fv
    ```