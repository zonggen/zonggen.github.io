---
layout: post
title:  "Note on #Git"
categories: [ blog, work]
featured-img: work-update-2
---

Note on `git`:

Pretty print the contents of the commit logs in a given format:
 - `git show --format=fuller`
 - `git commit --amend --author "Allen Bai <abai@redhat.com>"`

 Test a PR locally:
 - `git fetch <remote> pull/<id>/head` (check [this](https://github.com/TeamPorcupine/ProjectPorcupine/wiki/How-to-Test-a-Pull-Request) out)

 Other notes:
 - `git show --format=fuller FETCH_HEAD`
 - `git checkout <previous commit_id> <file_name>`
 - `git show --stat HEAD`
