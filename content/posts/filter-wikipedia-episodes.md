+++
title = "Back to Bash: Reflections on Filtering Wikipedia Episode Links a Year Later"
date = "2023-03-01"
tags = ["bash", "scripting", "linux"]
description = "Tired of manually renaming TV show episodes you've torrented? Check out this script I created that uses Wikipedia to automatically filter episode names, saving you time and effort."
+++

# How I Extracted TV Episode Titles Using Command Line Magic

I enjoy watching TV shows and prefer to torrent them for offline viewing. The issue is that these shows often have strange names that don't make sense and can be difficult to keep track of, especially since various individuals and groups post them on torrent sites. While I can use Wikipedia to obtain the actual episode names, manually copying and renaming each episode can be time-consuming. Therefore, I decided to automate the process using command-line tools and Ranger's bulk renaming feature.

## The Problem

First, I needed to find a way to scrape the episode title from a Wikipedia page. After some research, I discovered that the best way to do this was to download the page's source code and then extract the relevant information using a tool like grep.

## The Solution

I started by writing a simple curl command that would download the source code of the Wikipedia page for a given TV show:

```bash
curl -s "$1?action=raw"
```

This command uses the -s flag to suppress the output of curl, and $1 is the URL of the Wikipedia page. The ?action=raw part of the URL ensures that we get the raw source code of the page, rather than the formatted HTML.

Next, I needed to extract the episode title from the source code. After looking through the code, I found that each episode title was surrounded by a tag that looked like this:

```bash
== "Title" ==
```

To extract this information, I used grep to search for the tag and then extracted the episode title using sed. Here's the final command:

```bash
curl -s "$1?action=raw" | grep -B10 'ShortSummary' | grep -w 'Title' | sed 's/.*Title.*= //' | nl -w6 -w1 -s " - "
```

Let's break this command down:

- `bash curl -s "$1?action=raw"`downloads the source code of the Wikipedia page.

- `grep -B10 'ShortSummary'`searches for the line that contains the string "ShortSummary" and returns the 10 lines before it.

- `grep -w 'Title'` searches for the line that contains the word "Title" and returns it.

- `sed 's/.*Title.*= //'` removes everything before the episode title.

- `nl -w6 -w1 -s " - "` adds numbering to the output.
  With this command, I could simply pass in the URL of a TV show's Wikipedia page, and it would return a numbered list of all the episode titles.

  Then, I can simply copy these names and use Ranger's bulk rename feature to rename them.

## Conclusion

Through some trial and error, I was able to come up with a simple command-line script that makes my life a little bit easier. I'm excited to keep exploring new ways to use command-line tools to solve everyday problems.

- [**Link to the script**](https://github.com/prateekpunetha/dotfiles/blob/master/bin/bin/eplist)

I hope you found this post helpful, and feel free to reach out to me if you have any questions or feedback!
