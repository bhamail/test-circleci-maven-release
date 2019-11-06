# test-circleci-maven-release

[![CircleCI](https://circleci.com/gh/bhamail/test-circleci-maven-release.svg?style=svg)](https://circleci.com/gh/bhamail/test-circleci-maven-release)

A toy project for use in testing the process of releasing a maven project from CircleCI.

## Useful Hoops
Some nasty, but useful hoops through which one can jump

#### Extract inline orb
The command below will print the inline-orb by itself, which allows you to copy/paste that stand-alone orb elsewhere 
(e.g. to [src/orb.yml](https://github.com/sonatype-nexus-community/circleci-maven-release-orb/blob/master/src/orb.yml)).

    circleci config process .circleci/config-inline.yml > .circleci/local-config.yml  \
        &&  circleci local execute --config .circleci/local-config.yml --job 'extract-job' \

#### Run local "dry-run" CI build
A command similar to the one below will execute a 'dry-run' of a local CI build using the inline Orb.

    circleci config process .circleci/config-inline.yml > .circleci/local-config.yml  \
        &&  circleci local execute --config .circleci/local-config.yml --job 'my-inline-maven-release-orb/run-maven-release' \
            -e SECRING_GPG_ASC_BASE64='your base64 encoded key' \
            -e GITHUB_USERNAME='your username' \
            -e GITHUB_EMAIL=your-email@example.com \
            -e GITHUB_FINGERPRINT='github.com ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAq2A7hRGmdnm9tUDbO9IDSwBK6TbQa+PXYPCPy6rbTrTtw7PHkccKrpp0yVhp5HdEIcKr6pLlVDBfOLX9QUsyCOV0wzfjIJNlGEYsdlLJizHhbn2mUjvSAHQqZETYP81eFzLQNnPHt4EVVUh7VfDESU84KezmD5QlWpXLmvU31/yMf+Se8xhHTvKSCZIFImWwoG6mbUoWf9nzpIoaSjB+weqqUUmpaaasXVal72J+UX2B+2RPW3RcT0eOzQgqlJL3RKrTJvdsjE3JEAvGq3lGHSZXy28G3skua2SmVi/w4yCE6gbODqnTWlg7+wC604ydGXA8VJiS5ap43JXiUFFAaQ==' \
