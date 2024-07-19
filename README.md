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

## Samples

You can copy workflow files from [samples](https://github.com/ProjectTorreyPines/workflows/tree/master/samples) directory to your project repo's `.github/workflows/` directory to get started with default settings. Nothing else should be required to do.

## Badges

It is fun to decorate your README page to show that all CIs are running fine in the master branch. Add following raw code to the top of your repo's `README.md`:
```
![Format Check](https://github.com/ProjectTorreyPines/repo_name/actions/workflows/format_check.yml/badge.svg)
![Docs](https://github.com/ProjectTorreyPines/repo_name/actions/workflows/make_docs.yml/badge.svg)
![Tests](https://github.com/ProjectTorreyPines/repo_name/actions/workflows/test.yml/badge.svg)
```