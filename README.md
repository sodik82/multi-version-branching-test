# Multi version/release branching explained

1. Work on feature A and B is started (both planned for release 1)
2. Feature A is (squashed) and merged after review to main
3. Release 1 branch is started to allow development on feature C (targeted for release 2) while waiting for feature B and results of integration testing.
4. Feature C is already merged into main.
5. Feature B is squash-merged into release 1 after conflict was resolved (typical concurrent development conflict)

```bash
sodik@actopus:~/projects/PLAYGROUND/multi-version-branching-test (feature/feature-B)$ git merge release/1
Auto-merging src/controller.txt
CONFLICT (content): Merge conflict in src/controller.txt
Automatic merge failed; fix conflicts and then commit the result.
```

6. We need to merge changes from release 1 to main but have conflict (with feature C) again. We create chore branch for upmerge to check CI before merge into main. 
7. We resolve conflicts on chore branch and once CI passed, we were able to squash-merge it to main (which will shown to be a bad thing)
8. Release 2 branch was started
9. Hotfix from integration was fixed in release 1 branch - luckily it was in service not changed in between
10. We want to merge release 1 to release 2 (and later to main) but there are still conflicts we already resolved!

```bash
sodik@actopus:~/projects/PLAYGROUND/multi-version-branching-test (chore/release1-to-release2)$ git merge release/2
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Auto-merging src/cheese-service.txt
CONFLICT (add/add): Merge conflict in src/cheese-service.txt
Auto-merging src/controller.txt
CONFLICT (content): Merge conflict in src/controller.txt
Automatic merge failed; fix conflicts and then commit the result.
```

After resolve we see there are actually no real changes but git doesn't resolve them automatically.
This time we wan't do squash - just merge

11. Hotfix 2 was done on release 1
12. We start another up-merge branch - there are conflicts - but git can resolve them automatically now

```bash
sodik@actopus:~/projects/PLAYGROUND/multi-version-branching-test (chore/release1-to-release2-2nd)$ git merge release/2
Merge made by the 'ort' strategy.
 README.md             | 17 +++++++++++++++++
 src/controller.txt    |  4 ++++
 src/peace-service.txt |  7 +++++++
 src/world-service.txt |  2 +-
 4 files changed, 29 insertions(+), 1 deletion(-)
 create mode 100644 src/peace-service.txt
```
