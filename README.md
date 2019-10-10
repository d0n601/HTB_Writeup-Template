# Hack The Box CTF Writeup Template
This repository contains a template/example for my [Hack The Box](https://hackthebox.eu) writeups. Below you'll find some information on the required tools and general workflow for generating the writeups. I also write about it on my blog [here](https://ryankozak.com/how-i-do-my-ctf-writeups/), which has some details about also posting the markdown on Jekyll.

## Installation on Ubuntu 18.04
*Note: If you use Debian or Mint it may work but your mileage here might vary.*

1. Install [Latex](https://www.latex-project.org/) via `sudo apt-get install texlive`.
2. Install extra support packages for Latex  `sudo apt install texlive-xetex`.
3. Install [Pandoc](https://pandoc.org/) via `sudo apt-get install pandoc`.
4. Install the [Pandoc Latex Template](https://github.com/Wandmalfarbe/pandoc-latex-template)
   * Download the latest version of the Eisvogel template from the [release page](https://github.com/Wandmalfarbe/pandoc-latex-template/releases/latest).
   * Extract the `tar.gz` archive and open the folder.
   * Create a pandoc templates folder if it doesn't exist at `~/.pandoc/templates/`.
   * Move the template `eisvogel.tex` to your pandoc templates folder and rename the file to `eisvogel.latex`.
5. Make sure you have [PDFtk](https://www.pdflabs.com/tools/pdftk-the-pdf-toolkit/) installed via `sudo snap install pdftk`.


## Usage
Initially I publish my writeups as a password protected pdf, the password set to the root flag for the box. After the box is retired, I post the writeup on my Jekyll site.

Here's the directory structure for my writeup [template](https://github.com/d0n601/HTB_Writeup-Template).

```
HTB_Writeup-TEMPLATE
│   HTB_Writeup-TEMPLATE-d0n601.md   
│
└───pdf
│   │   HTB_Writeup-TEMPLATE-d0n601.pdf
│   │
│   └───protected
│       │   HTB_Writeup-TEMPLATE-d0n601.pdf
│   
└───images
│       │   badge.png
│       │   someotherimage.png
│       │   ...
```

### Markdown for pdf
In order to generate a pdf from markdown using pandoc we must format the header correctly. The header for my template is as follows.

```
---
title: "Hack The Box - BOX NAME HERE"
author: Ryan Kozak
date: "2019-08-11"
subject: "CTF Writeup Template"
keywords: [HTB, CTF, Hack The Box, Security]
lang: "en"
titlepage: true
titlepage-text-color: "FFFFFF"
titlepage-color: "0c0d0e"
titlepage-rule-color: "8ac53e"
logo: "./images/badge.png"
logo-width: 350
...
```

Once the writeup is complete, or you're just looking to build it to see how it's looking as a pdf, issue the following command from your writeup directory.

`pandoc --latex-engine=xelatex ./HTB_Writeup-TEMPLATE-d0n601.md -o ./pdf/HTB_Writeup-TEMPLATE-d0n601.pdf --from markdown --template eisvogel --listings`


### Password Protect pdf
Once the writeup is complete and ready to publish, it should be protected with the root flag so it doesn't violate [Hack The Box](https://hackthebox.eu) rules, allow people to cheat, and generally spoil the fun.

To password protect the pdf I use `pdftk`. From the root folder of the writup directory issue the following command.

`pdftk ./pdf/HTB_Writeup-TEMPLATE-d0n601.pdf output ./pdf/protected/HTB_Writeup-TEMPLATE-d0n601.pdf user_pw v5gw5zkh8rr3vmye7p4ka`

Now a password protected pdf will appear in the `/pdf/protected` directory.
