---
title: Terminology
description: GRGate terminology
lead: ""
draft: false
images: []
menu:
  docs:
    parent: overview
weight: 200
---

Different terminology is used by different provider for what is called an
unpublished release:

- **GitHub** uses the term [draft releases][draft-release] to prepare a release
without publishing it.
- **GitLab** uses the term [upcoming releases][upcoming-release], it is similar
to GitHub Pre-releases where a badge notify the upcoming release in the GitLab
release page.  The attribute `released_at` should be set to a future date to
have it enabled and it is only possible to change it using the GitLab API.

[draft-release]: https://docs.github.com/en/github/administering-a-repository/managing-releases-in-a-repository#about-release-management
[upcoming-release]: https://docs.gitlab.com/ee/api/releases/#upcoming-releases
