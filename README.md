# Git secrets check

This repository is a Jenkinsfile which periodically runs git secrets against a test file. The test file contains 3 fake secrets.

* A fake AWS account number
* A fake AWS secret key
* A public AWS account number

This needs to be in its own repository because all of our other repositories have a build check which runs git secrets so if this file was in there, all future build checks would fail.