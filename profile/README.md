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

### How to Merge Code
Once you have developed a feature/fix that is ready to be merged to production, you should raise a Pull Request (PR) to the `main` branch. This will trigger the PR pipeline on Jenkins to run both unit tests and code security scan. 

Once both checks pass, you may merge it into production.

You will see the following information returned by the Snyk Code Security Scanner when vulnerabilities are detected:

<img width="1111" alt="image" src="https://github.com/user-attachments/assets/5165c79f-0fe1-4ac6-8337-ec36e308b9a9">

By default, Snyk Code Security will block your PR if it detects a vulnerability that is classified as **high**.

### How to Deploy to Production
By convention, the pipeline is setup such that you do not need to worry about deployment as it does all the heavy lifting for you.

When you merge your changes to `main`, the merge triggers the deployment pipeline on Jenkins to build and push Docker images to Docker Hub, which it will then use to perform rolling update on the production VM.

### Onboarding Repositories to Jenkins Pipeline
* You should have setup unit tests to test out granular functionailities of your app.
* You should have `Dockerfile` ready for image build and deployment.


### Pipeline status
For every PR raised or merged, Jenkins will raise an issue in the respective repo's `Issue` section under the section. Here is an example:

<img width="1386" alt="image" src="https://github.com/user-attachments/assets/c901530c-c575-4fd4-9e64-51f241ee49a9">

### Commit Message
Write meaningful commit messages that summarize the changes in this commit. Start your commit message with an uppercase verb in present tense, e.g `Update database schema`.
