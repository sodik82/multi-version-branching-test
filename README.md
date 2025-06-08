# Multi version/release branching explained

1. Work on feature A and B is started (both planned for release 1)
2. Feature A is (squashed) and merged after review to main
3. Release 1 branch is started to allow development on feature C (targeted for release 2) while waiting for feature B and results of integration testing.
4. Feature C is already merged into main.
5. Feature B is squash-merged into release 1 after conflict was resolved

```bash
sodik@actopus:~/projects/PLAYGROUND/multi-version-branching-test (feature/feature-B)$ git merge release/1
Auto-merging src/controller.txt
CONFLICT (content): Merge conflict in src/controller.txt
Automatic merge failed; fix conflicts and then commit the result.
```

