# GitHub Actions Workflows
Central repository to store workflows used by some of the project repositories.

## Available workflows:

All workflows currently use latest julia subversion of v1 and run on x64 architecture in ubuntu-latest image.

### 1. **Compat Helper**
Installs compat helper which checks for updates in dependencies based on compat entries in `Project.toml` and sends a PR to dev branch if a dependency has updated version available.
* Typically used with cron schedule, called from master branch.

### 2. **Format Check**
Uses [JuliaFormatter](https://github.com/domluna/JuliaFormatter.jl) to check if the julia files conform with `.JuliaFormatter.toml` configuration in a repo.
* Typically used with PR and push to `master` and `dev`.
* Good to set path specifier to reduce triggering to only `.jl` changes.

### 3. **Documentation**
Uses [Documenter](https://github.com/JuliaDocs/Documenter.jl) to test if documentation making is working fine and deploys documentation based on `docs/make.jl` settings.
* Typically used with PR and push to `master` and `dev`.
* Good to set path specifier to reduce triggering to only `src/**` and `docs/**` changes.

### 4. **TEST**
Uses  [https://github.com/julia-actions/julia-runtest](https://github.com/JuliaDocs/Documenter.jl) to run `test/runtests.jl`
* Typically used with PR and push to `master` and `dev`.
* Good to set path specifier to reduce triggering to only `src/**`, `test/**`, and `Project.toml` changes.

**Caution**: do the following steps only if you know what you are doing. Ask `guptaa@fusion.gat.com` for help if you need.:
* For pulling the test sample files, this workflow will use `dvc` from [SOLPSTestSamples](https://github.com/ProjectTorreyPines/SOLPSTestSamples) repo.
* This feature is on by default. If your testing does not require sample files from [SOLPSTestSamples](https://github.com/ProjectTorreyPines/SOLPSTestSamples), then turn this off by adding `use_dvc: false` in `with` field. See sample file for example.
* Your repo must have following 4 secret variables with the exact same name as described below:
  * `DVC_KNOWN_HOSTS` : know_hosts entry lines for cybele, omega, and iris.
  * `DVC_SSH_CONFIG`: ssh config entries for cybele, iris, and omega with username, port, and proxy command.
  * `DVC_SSH_KEY`: Private rsa ssh key whose public part has been added to `cybele:/home/username/.ssh/authorized_keys`, and similarly to omega and iris.
  * `SOLPSTESTSAMPLES_SSH_KEY`: Private rsa ssh key whose public part has been stored in Deploy Keys of SOLPSTestSamples repo.

## Samples

You can copy workflow files from [samples](https://github.com/ProjectTorreyPines/workflows/tree/master/samples) directory to your project repo's `.github/workflows/` directory to get started with default settings. Nothing else should be required to do.

## Badges

It is fun to decorate your README page to show that all CIs are running fine in the master branch. Add following raw code to the top of your repo's `README.md`:
```
![Format Check](https://github.com/ProjectTorreyPines/repo_name/actions/workflows/format_check.yml/badge.svg)
![Docs](https://github.com/ProjectTorreyPines/repo_name/actions/workflows/make_docs.yml/badge.svg)
![Tests](https://github.com/ProjectTorreyPines/repo_name/actions/workflows/test.yml/badge.svg)
```