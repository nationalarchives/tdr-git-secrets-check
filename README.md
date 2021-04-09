# Git secrets check

This repository is a Jenkinsfile which periodically runs git secrets against a test file. The test file contains 3 fake secrets.

* A fake AWS account number
* A fake AWS secret key
* A public AWS account number

This needs to be in its own repository because all of our other repositories have a build check which runs git secrets so if this file was in there, all future build checks would fail.

The job runs git-secrets twice. Once to get the exit code, which should be non-zero as it should have found secrets in the test file and once to get the line numbers of the secrets in the file to make sure that it is finding the correct secrets.
There is also a post failure block so we get notified if the job itself fails. 