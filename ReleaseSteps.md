

# Release VexFlow 4.1.0
_Ron Yeh: This section documents how I tested and released VexFlow 4.1.0._

First, check that I'm in the correct repository folder on my computer.

```
git remote -v
```
```
origin	git@github.com:ronyeh/vexflow.git (fetch)
origin	git@github.com:ronyeh/vexflow.git (push)
upstream	git@github.com:0xfe/vexflow.git (fetch)
upstream	git@github.com:0xfe/vexflow.git (push)
```

Pull down new changes (e.g., recent PR merges). Hopefully there aren't any since the most recent release candidate!

```
git fetch upstream
git rebase upstream/master
npm ci
```

Clean my local build.

```
grunt clean
```

Let's build it, and take a look at the demos.

```
grunt
```

Done building. I open the `vexflow/build/` folder to visually inspect the output. Looks good. I see some output files related to the Leland font, which is new in 4.1.0.

There are a some examples inside the `vexflow/demos/` folder. They look good to me!

Also, let's check the browser unit tests in `vexflow/tests/flow.html`.

```
open tests/flow.html
```

The test page says:

```
Tests completed in 18881 milliseconds.
9931 assertions of 9931 passed, 0 failed.
```

Open my 2-factor authentication app so I can push to npm.

Alright, let's run grunt release! The GITHUB_TOKEN in the next command is unique to each user, so you'll need to generate your own.

```
GITHUB_TOKEN=ghp_xxxxxxxxxxxxxxxx    grunt release
```

Use the arrow keys to select the correct release.

```
? Select increment (next version): (Use arrow keys)
❯ patch (4.1.0)
  minor (4.1.0)
  major (5.0.0)
  prerelease (4.1.0-rc.1)
  Other, please specify...
```

Lots of stuff happens.

```
? Publish vexflow to npm? Yes
? Please enter OTP for npm: xxxxxxx
? Commit (Release VexFlow 4.1.0)? Yes
? Tag (4.1.0)? Yes
? Push? Yes
? Create a release on GitHub (4.1.0)? Yes
```

Released!

After using our release-it script, there are always 2 local commits that I need to push upstream.

```
commit 7067aefe668b2f87a6d7ecb0ea35c8e57b11a7ce (HEAD -> master, origin/master, origin/HEAD)
Author: Ron B. Yeh
Date:   Thu Dec 1 17:17:33 2022 -0800

    Remove build/ after releasing version 4.1.0 to npm and GitHub.

commit 1c1e4cf36ea037fb25cffca1fca96a303d09edb2 (tag: 4.1.0)
Author: Ron B. Yeh
Date:   Thu Dec 1 17:17:22 2022 -0800

    Release VexFlow 4.1.0

^^^^^^^ THE ABOVE TWO COMMITS NEED TO BE PUSHED UPSTREAM ^^^^^^^

commit a696355e15caddaff44c05e861991a5d355a8189 (upstream/master)
Author: Ron B. Yeh
Date:   Wed Nov 30 00:07:21 2022 -0800

```

Someday we will need to figure out how to automate this. It might be as simple as adding "`git push upstream`" to the script. However, we'd need to also handle the case where the user wants to push to the main repo, so the command might be "`git push`".

Here, I'm in my personal repository's folder, so I need to push upstream to the 0xfe repo.

```
git push upstream
```

All done!