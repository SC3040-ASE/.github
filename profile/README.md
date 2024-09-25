# SC3040

## Links
- Asana: https://app.asana.com/0/1208082719272721/1208082720271251
- SharePoint: https://entuedu.sharepoint.com/sites/ASWE/SitePages/CollabHome.aspx?e=1:7a058cedbefc44049b604299db911607
- Jenkins: http://20.6.107.48:8080/

## DevOps
### Branching Convention
Try to follow the following conventions when managing branches:
* The default production branch should be `main`. This is important as many Jenkins pipeline are configured to listen to changes on the `main` branch. Setting it to the default `master` branch may break some of the pipelines.
* For feature development, checkout from the `main` branch, then name your branch with the name `feature/<your new shiny feature>`
* For hotfixes, checkout from the `main` branch, then name your branch with the name `hotfix/<your bandaid to the problem>`

### Continuous Integration
By convention, a CI job is triggered for every PR raised, and subsequent commits to the same PR re-triggers the job. The job will annotate the PR with checkpoints such as `unit_test_running`, `quality_scan_running` and `security_scan_running`. When the CI job passes, the PR is annotated with `ci_passed`, indicating that your PR has successfully passed the automated unit tests, quality tests and security scan.

The Jenkins bot will also comment on the PR, relevant information such as quality scan result (with a reference link to the SonarQube report), and Snyk security scan result.

### Continuous Deployment
Once your PR is ready for merge, simply annotate your PR with the label `build_ready`. This will flag the PR for build sign-off. When the CD job is triggered, the pipeline will be annotated with the appropriate comments informing you the current checkpoints reached. 

If your PR did not pass the CD build process, simply follow the problem described either by Jenkins bot in the PR, or follow the build URL to trace the origin of the problem. Once solved, you can re-trigger the CD build job by re-annotating the PR with the `build_ready` label.

### Commit Message
Write meaningful commit messages that summarize the changes in this commit. Start your commit message with an uppercase verb in present tense, e.g `Update database schema`.
