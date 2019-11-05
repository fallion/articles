# GoReleaser + Drone + Github: Tutorial

Couple of days ago I was looking to set up https://goreleaser.com.
At first I tried Travis, however I like stuff simple and Travis was giving me a hard time with the releaser flow. That's when I came across https://dev.to/mstrsobserver/painless-github-releases-with-drone-and-goreleaser-45b7 (kudos to @mstrsobserver btw), which unfortunately did not work with 1.0 version of Drone.

So… I decided to write this instead.

## Why GoReleaser?

GoReleaser is a nice little app that will generate Go binaries, and the changelog between tags.

What are git tags? It's the way that git has to "bookmark" specific commits on a repository's history as something that has certain interest, that's why it's usually used for marking releases, where the tag it's specifying the version.

What is drone? Drone is a Continuous Integration app like Travis, Gitlab CI and Circle CI. It lets you make sure that your commits fulfil your requirements before being merged/released.

### Step 1: Set up a Go project

This part is fairly simple just create a main.go file and put something in it. Like so:

Push this to a new Github repo.

### Step 2: Set up Goreleaser

Everything can be found here: https://goreleaser.com
Essentially for OSX it's this:
// Terminal
brew install goreleaser/tap/goreleaser
goreleaser init
This will create a sample goreleaser config. Adjust to your liking and then push it to your Github repo.

### Step 3: Set up Drone

Create a configuration for Drone by creating a .drone.yml file in the root of your repository.
Drone allows you test and ship stuff (using GoReleaser) with confidence. I highly recommend locking down your master branch and only allowing Pull Requests that pass Drone to be merged into master.

Sample config: (better formatted can be found here: https://github.com/Fallion/go-template/blob/master/.drone.yml)

Push this file to your Github repo.

**Next steps:**

- go to https://cloud.drone.io/
- connect Drone with your Github account
  go to https://github.com/settings/tokens and create a token with repo access (This allows GoReleaser to add changelogs and binaries to your Github)
- go back to Drone
- go to the dashboard and activate your project
- go to project settings
- add github_token secret where the value is the token from Github (see screenshot)

### Step 4: Release

Create a new tag in your repo. This will trigger the Drone pipeline and GoReleaser will automatically add a changelog as well as the built binaries for you project and you can go party!

If you come across any issues feel free to ping me at https://twitter.com/fallion.
