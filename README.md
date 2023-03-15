# test-actions
To test github actions

|               | Current Status                                                                                                                                                                                                                                                                                                                                                 |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Build         | [![Build Status](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2Fjorgesanchezperez%2Ftest-actions%2Fbadge%3Fref%3Dmaster%26token%3Dad528ab8e662c0c3ee86e88fbbdeca49fb032526&style=flat-square)](https://actions-badge.atrox.dev/jorgesanchezperez/test-actions/goto?ref=master&token=ad528ab8e662c0c3ee86e88fbbdeca49fb032526) |
| Code coverage | [![codecov](https://codecov.io/gh/OpenBankingToolKit/cdr-standards-model/branch/master/graph/badge.svg)](https://codecov.io/gh/OpenBankingToolkit/cdr-standards-model)                                                                                                                                                                                         |
| Release       | [![GitHub release](https://img.shields.io/github/release/jorgesanchezperez/test-actions.svg)](https://GitHub.com/jorgesanchezperez/test-actions/releases/)                                                                                                                                                                                                     |
| Release       | [![GitHub release](https://img.shields.io/github/v/release/jorgesanchezperez/test-actions?sort=semver)](https://GitHub.com/jorgesanchezperez/test-actions/releases/)                                                                                                                                                                                           |
| Tag           | [![GitHub release](https://img.shields.io/github/v/tag/jorgesanchezperez/test-actions?sort=semver)](https://GitHub.com/jorgesanchezperez/test-actions/tags/)                                                                                                                                                                                                   |
| License       | ![license](https://img.shields.io/github/license/ACRA/acra.svg)                                                                                                                                                                                                                                                                                                |

### Squash commits into one
https://www.internalpointers.com/post/squash-commits-into-one-git

```shell
git rebase --interactive ${commit-hash}
```
```shell
git rebase --interactive HEAD~N
```
**Shorter**
```shell
git rebase -i ${commit-hash}
```
```shell
git rebase -i HEAD~N
```
>Where N is the number of commits you want to join, starting from the most recent one

## Create release
```shell
git checkout -b release/1.0.0
mvn versions:set -DremoveSnapshot
mvn versions:set-property -Dproperty=maven-release-plugin.version,git-changelog-maven-plugin.version -DnewVersion=8.0.0 
# Update dependencies manually
mvn clean package # to test the integrity of the project
git add .
git commit -m "Release candidate ...."
git push
git tag rc1.0.0 # release candidate
git push origin rc1.0.0 # to push the tag to github
# run the release github action workflow
mvn versions:set -DnextSnapshot # update the version release to development iteration
git add .
git commit -m "....."
git push # to push the latest changes to the release branch
# Create the proper PR to merge the release branch into master 
mvn versions:commit # delete pom backups accepting the changes
mvn versions:revert # restores the poms from the pom backups
```