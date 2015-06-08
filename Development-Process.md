It is the responsibility of IoT.js Maintainers and Committers to decide whether submitted code should be integrated into the master branch, returned for revision, or rejected.

Individual developers maintain a local copy of the IoT.js codebase using the git revision control system. Git ensures that all participants are working with a common and up-to-date code base at all times. Each developer works to develop, debug, build, and validate their own code against the current codebase, so that when the time comes to integrate into the master branch of the project, their changes apply cleanly and with a minimum amount of merging effort.

### Proposals, Get Answers and Report a Bug via Github Issues

If you have a question about IoT.js code, have trouble any documentation, would like to suggest new feature, or find a bug, [review the current IoT.js issues](https://github.com/Samsung/iotjs/issues) in GitHub, and if necessary, [create a new issue](https://github.com/Samsung/IoT.js/issues/new).

**There are several labels on the Issue. Please choose proper labels on the purpose.**
* **bug**
* **community** : any issues on the community operation
* **enhancement** : feature enhancement proposal
* **help wanted**
* **new feature request(proposal)** : new feature proposal
* **project announcement** : general announcement on the project such as new release, new Maintainer/Committer and so on
* **question** : any questions on the project

and so on.

### Feature development process

The IoT.js Project development process is marked by the following highlights:
* The feature development process starts with an author discussing a proposed feature with the Maintainers and Committers
  - Open the issue with label 'new feature request(proposal)'
* The Maintainers and Committers evaluate the idea, give feedback, and finally approve or reject the proposal.
* The author shares the proposal with the community via **_Github issues with 'new feature request' label_**
* The community provides feedback which can be used by the author to modify their proposal and share it with the community again.
* The above steps are repeated until the community reaches a consensus according to the [Community Guidelines](Community-Guidelines).
* After a consensus is reached, the author proceeds with the implementation and testing of the feature.
* After the author is confident their code is ready for integration:
  - The author generates a patch and signs off on their code.
  - The author submits a patch according to the [Patch Submission Process](Patch-Submission-Process).
* The Maintainers and Committers watch the pull request for the patch, test the code, and accept or reject the patch accordingly.
* After the code passes code review, the Maintainers and Committers accept the code(integrated into the master branch), which completes the development process.
* After a patch has been accepted, it remains the authoring developer's responsibility to maintain the code throughout its lifecycle, and to provide security and feature updates as needed.


### Tips on GitHub Issues

* Check existing [IoT.js issues](https://github.com/Samsung/IoT.js/issues) for the answer to your issue.
Duplicating an issue slows you and others. Search through open and closed issues to see if the problem you are running into has already been addressed.
* If necessary, [open a new issue](https://github.com/Samsung/IoT.js/issues/new).
  - Clearly describe the issue. 
     + What did you expect to happen?
     + What actually happened instead?
     + How can someone else recreate the problem?
  - Include system details(such as the hardware, library, and operating system you are using and their versions).
  - Paste error output and logs in the issue or in a Gist(https://gist.github.com/). 

For more information about GitHub issues, refer to the [GitHub issues guidelines](https://guides.github.com/features/issues/).