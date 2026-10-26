# Definition of Done

An issue is **Done** only when every item is true:

- [ ] All acceptance criteria in the issue are met
- [ ] New logic has unit tests, and all tests pass locally
- [ ] CI is green on the pull request
- [ ] The diff has been self-reviewed in the PR (no debug code, no commented-out code)
- [ ] No `TODO` left in the code without a linked issue
- [ ] Docs are updated if behaviour changed (README, ADR, CHANGELOG)
- [ ] The PR is merged into `main`, the branch is deleted and the issue is closed
