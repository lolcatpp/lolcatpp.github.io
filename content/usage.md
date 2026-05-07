---
title: "Usage"
date: 2026-05-07
draft: false
ShowToc: true
TocOpen: true
---

## Basics

```bash
echo "hello, world" | lolcat
```

<picture>
  <source srcset="/example-dark.jpg" media="(prefers-color-scheme: dark)">
  <img src="/example-light.jpg" alt="lolcat++ example output">
</picture>

## Options

| Flag                | Default | Description                           |
| ------------------- | ------- | ------------------------------------- |
| `-p`, `--spread`    | `3.0`   | Rainbow spread                        |
| `-F`, `--freq`      | `0.1`   | Rainbow frequency                     |
| `-S`, `--seed`      | `0`     | Rainbow seed (`0` = random)           |
| `-a`, `--animate`   | off     | Enable animation                      |
| `-d`, `--duration`  | `12`    | Animation duration                    |
| `-s`, `--speed`     | `300.0` | Animation speed                       |
| `-i`, `--invert`    | off     | Invert colors (color the background)  |
| `-t`, `--truecolor` | off     | Force 24-bit truecolor mode           |
| `-f`, `--force`     | off     | Force color output (e.g. when piping) |
| `-h`, `--help`      | N/A     | Show help                             |
| `-v`, `--version`   | N/A     | Show version                          |

## Examples

```bash
# pipe anything
ls -la | lolcat

# rainbow several files
lolcat README.md LICENSE

# tighter rainbow
echo "hello" | lolcat --spread 1.0 --freq 0.3

# animate
echo "hello, world" | lolcat -a -d 5

# invert (color the background, not the text)
echo "hello" | lolcat --invert

# force color when piping into less
ls --color=always | lolcat -f | less -R
```

## Why C++?

The original [lolcat](https://github.com/busyloop/lolcat) is a Ruby script.
lolcat++ aims to be drop-in compatible while being **faster** ---
nice when you want to use it in init scripts, motd output, or anywhere the Ruby startup time becomes noticeable.

Also, why not?
