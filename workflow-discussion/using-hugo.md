# Getting Started with Hugo: First Step Toward Automation

## Download Hugo 

There are three main ways to download hugo:

1. [Prebuilt binaries](https://gohugo.io/installation/windows/#prebuilt-binaries): These are zip files that you can extract to obtain executables(called binaries).
2. [Package Managers](https://gohugo.io/installation/windows/#package-managers): These are tools that can install hugo with a single command, these may or may not be already present in your Operating system, 
	
	- for Linux: [See all tools, its worth it have a look](https://gohugo.io/installation/linux/#package-managers)
	- for windows: `Chocolatey`, `Scoop`, `Winget`
	- for MacOS: `Homebrew`, `MacPorts`
	
3. [Build from Source](https://gohugo.io/installation/windows/#build-from-source): It means compiling a software from the source code instead of pre-compiled or pre-built version like an executable(prebuilt-binaries)

4. [Use Docker](https://github.com/gohugoio/hugo/pkgs/container/hugo/280590856?tag=v0.135.0): Docker allows you to create a consistent and isolated environment to run Hugo without needing to install it directly on your system. When you run Hugo with Docker, you're using a containerized version of Hugo, which means Docker provides a virtual environment where Hugo runs as if it's on its own mini-operating system. This ensures:

- No local dependencies: You don't need to worry about installing Go, C compilers, or any other tools. Everything is pre-packaged within the Docker container.
- Cross-platform consistency: Docker makes it easy to run Hugo across different operating systems (Windows, macOS, Linux) while maintaining the same environment. Your project behaves the same on any machine with Docker.
- Quick setup: You can run a Hugo website instantly using a simple Docker command, without needing to manage installations or environment configurations.  

Running Hugo in a Docker container is especially useful if you want to avoid potential conflicts with other software on your machine or if you're automating your site builds in a continuous integration (CI) pipeline.

[Compare all the first three ways](https://gohugo.io/installation/windows/#comparison)

## Usage

1. Run ```hugo new site mysitedirectoryname```
2. Follow the instructions on the screen(by hugo) and play the game

Refer the [hugo site](https://gohugo.io/about/introduction/) for any questions.  
Hit `ctrl+f` to find what you need or use AI.
