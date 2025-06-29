---
layout: gallery
title: "Clap Game Engine"
date: 2025-06-30
categories: [clap]
header:
  overlay_image: /assets/img/banner-matrix.png
  overlay_filter: rgba(0,0,0,0.3)
---

# [Clap: a 3D game engine in C](https://github.com/virtuoso/clap/)

[![linux-build](https://github.com/virtuoso/clap/actions/workflows/linux-build.yml/badge.svg?branch=main)](https://github.com/virtuoso/clap/actions/workflows/linux-build.yml)
[![www-build](https://github.com/virtuoso/clap/actions/workflows/www-build.yml/badge.svg?branch=main)](https://github.com/virtuoso/clap/actions/workflows/www-build.yml)
[![macos-build](https://github.com/virtuoso/clap/actions/workflows/macos-build.yml/badge.svg?branch=main)](https://github.com/virtuoso/clap/actions/workflows/macos-build.yml)
[![windows-build](https://github.com/virtuoso/clap/actions/workflows/windows-build.yml/badge.svg?branch=main)](https://github.com/virtuoso/clap/actions/workflows/windows-build.yml)

- [What is Clap?](#what-is-clap)
  - [Show me!](#show-me)
  - [So, C?](#so-c)
  - [But Rust!](#but-rust)
  - [Having said that](#having-said-that)
- [Why is Clap?](#why-is-clap)
- [How to Clap?](#how-to-clap)
- [API](#api)
- [Versioning and release process](#versioning-and-release-process)
- [If you like weird and wonderful things](#if-you-like-weird-and-wonderful-things)
- [Screenshots](#screenshots)

# What is Clap?

[Clap](https://github.com/virtuoso/clap) is a lightweight multiplatform 3D game engine that aims to "_do more with less_", meaning procedurally generating/postprocessing things that it can, instead of purely relying on static assets (not that you can't utilize a static asset pipeline with it). The name comes from the koan (probably) that posits the question -- what is the sound of a clap with one hand, and I needed a word that starts with a "C", because it's written in C. Yes, I'm aware of [the colloquial meaning of clap](https://www.urbandictionary.com/define.php?term=clap "if you're here because of that, ask your doctor about a course of antibiotics").

Clap exists for 5 years now, though with dormant stretches -— the longest being over a year. Most recently, it powered [a full game jam title](https://ldjam.com/events/ludum-dare/57/towards-the-light) in Ludum Dare 57, the entirety of which lives in [`demo/ldjam57`](https://github.com/virtuoso/clap/tree/main/demo/ldjam57) of the main repository.

Clap takes care of:
- 3D rendering/lighting/postprocessing/compositing/etc
- input controls (keyboard/mouse, gamepads, touch screens)
- scene graph
- character movement
- collisions/"physics" (`ODE`)
- audio/SFX
- procedural generation of various things (meshes, color grading LUTs)
- packing assets
- runtime tweaking / editing pretty of much anything (model placement, lighting, all sorts of rendering options, etc).

More detailed and technical feature list should be somewhere on the [v0 release page](https://github.com/virtuoso/clap/releases/tag/v0).

Clap runs on Linux, Mac OS X (arm64, x86), Windows x64 and in a browser. That last one is especially important: the WASM/"HTML5" build is not an afterthought, but a first-class citizen, and (maybe having to cut corners here and there) will remain such.

## Show me!

Right here is a [live demo](http://ash.works/clap/main/ldjam57/) of our Ludum Dare 57 game. And [a whole lot more](https://github.com/virtuoso/clap#live-demos-and-executables) live demos and executables.
There are a few [screenshots](#screenshots) at the bottom of the page; [more screenshots here](clap-gallery.html) and a whole youtube video:

[![Watch the video](https://img.youtube.com/vi/nyvz55lmAHc/hqdefault.jpg)](https://youtu.be/nyvz55lmAHc)

## So, C?

Yes, it's written in C. There are several reasons for this:
- you can't beat the performance, memory footprint and compilation time of C, not with C++, not with Rust
- it's the language that I'm most comfortable with.

One could say that it's also the most portable language, but technically, C++ till take the cake there. Some platforms, while having a C compiler, lack the most rudimentary C library, so one has to compensate. And when I say "it's in C", I mean C23 with GNU extensions, in other words, it builds with modern GCC and Clang. Porting it to a platform that's locked on C89 will probably require pre-processing by some kind of a custom `sparse`-based uglifier.

Yes, I'd very much like to have closures and maybe function overloading, but then I'd be forced to make use of other C++ features, STL etc. Better `enum`s, pattern matching are sure cool, but from this distance they seem similar to a fully realtime raytraced reflection on the surface of a counter in "Oh Deer Diner": cool for about 30 seconds, but then you need to get on with things and it becomes completely irrelevant. 

## But Rust!

Nope. I'll be done with the game logic while a Rust programmer is still proving to the borrow checker that he's not a potato. Eloquent counterarguments like "skill issue" are all addressed in [this excellent writeup](https://loglog.games/blog/leaving-rust-gamedev/). If you happen to be a competent Rust programmer and a game developer, I tip my hat in your general direction (while keeping its mutable reference to myself). All the power to you!

## Having said that

There's obviously GLSL and cmake, which for better or worse *are* programming languages. Objective C is very much in the cards. Besides that, Clap leans heavily on [ODE](https://www.ode.org), [ImGui](https://github.com/ocornut/imgui) (via [cimgui](https://github.com/cimgui/cimgui)), [meshoptimizer](https://github.com/zeux/meshoptimizer), which are all written in C++. Most of them provide a C API, though. And no, there is no promise that in the future bits of C++ won't emerge.

# Why is Clap?

The reason it started was my fondness for "Breath of the Wild" (the wait for its sequel at that point was already bordering on ridiculous) and curiosity as to what it would take to make tech that can do that, but without the benefit of having hundreds of developers. I went into it completely clueless. Today, I *am* aware of all the things that are missing from Clap to make it BoTW-worthy. And at the same time, the priorities have shifted. I played other games since.

Today, Clap exists for
- building *weird*, *stylized*, *athmospheric* games
- *doing more with less*
- if at all possible, run on a toaster.

The roadmap, such as it is, is shaped with these design principles in mind.

Besides being educational, it has the enormous advantage of giving me complete control of every aspect of the engine when we're, for example, gamejammin'. And it's also ridiculously fun.

# How to Clap?

The easiest way is always to dive right in, grab [one of the demos](https://github.com/virtuoso/clap/tree/main/demo/) and start tinkering. There's a [CONTRIBUTING](https://github.com/virtuoso/clap/tree/main/CONTRIBUTING.md) document that covers the basics. The basic idea is to write code that's self-evident and doesn't require comments, which tend to go out of sync with reality. That said, using comments is encouraged —- as is adding them to existing code, which can also be a good way to learn the system.

# API

There's no API of the kind that one would expect of a library, as of this moment. This will change. This is not a top priority right now, because there are perfectly workable ways of getting your code to link with Clap, either by adding your game to `demo/` directory and having all the benefits of all the includes, compiler flags, linker flags etc for free, or you can add Clap as a submodule to your game and have more or less the same level of convenience.

The API that is there is in a permanent state of flux. This is very unlikely to change. Every time you fetch a new version, you'll likely have to fix up some things. Kind of like ImGui keeps its users on their toes by breaking its API between minor releases every few weeks. It's completely normal. Every time this happens, it's an opportunity to learn something new.

# Versioning and release process

There are no good versioning schemes in existence. Some are better than others, often due to how they tie in with the release process. Therefore, I went with the simplest thing: versions that increase monotonically from `v0` ad infinitum. There may be occasional version-looking tags, like `v0-pre1`: these are not versions or releases; their purpose is to mark a milestone in development, for example: this is where we are going into the next game jam.

There is no release process: features and bugfixes can be added at any time. A sufficient amount of new features since the previous release may trigger a release. A standalone fix for a monumental engine breaking / retina scorching bug may trigger a release. It took 5 years to get to `v0`. The next one may be next month.

# If you like weird and wonderful things

- Give us a star:
[![GitHub stars](https://img.shields.io/github/stars/virtuoso/clap?style=social)](https://github.com/virtuoso/clap)
- Join in!
  - There's a reasonably terse [contribution guidelines document](https://github.com/virtuoso/clap/blob/main/CONTRIBUTING.md)
  - There are [open issues](https://github.com/virtuoso/clap/issues) that are about as informal as possible: both bugs and things TODO are tracked there.

[v0 release](https://github.com/virtuoso/clap/releases/tag/v0)

# Screenshots

[![(basename f)](/assets/img/clap-hyper-sunset.png)](/assets/img/clap-hyper-sunset.png)
[![(basename f)](/assets/img/clap-comic-red.png)](/assets/img/clap-comic-red.png)
[![(basename f)](/assets/img/clap-matrix-ui2.png)](/assets/img/clap-matrix-ui2.png)
[Screenshot gallery](/clap-gallery.html)

---