# Gitlab Mirror

Gitlab Mirror will watch a GitLab group and keep it in sync with external git repositories.

## Usage

1. Create group on your gitlab instance or gitlab.com. e.g. `mirror-test`
2. Add a repository you like to sync to. e.g `my-project`
3. Add a description to the project in YAML format containing an `origin` field. e.g. `origin: https://git.example.org/my-project.git`
4. Execute  set the `GITLAB_PRIVATE_TOKEN` environment variable a personal access token or your private token and execute `gitlab-mirror`

``` sh
export GITLAB_PRIVATE_TOKEN="<personal-access-token>"
gitlab-mirror -g mirror-test
```

This will sync the group `mirror-test` on gitlab.com. If you want to sync a group on a diffetenr GitLab instance, use the `-u` flag.

``` sh
gitlab-mirror -g mirror-test -u http://gitlab.example.org
```

### Multiple concurrent jobs

`gitlab-mirror` allows to execute multiple mirror jobs in parallel using the `-c <n>` flag.

``` sh
gitlab-mirror -g mirror-test -c 8
```

This will execute at most 8 sync jobs in parallel

### Description format

For `gitlab-mirror` to mirror a repository it needs to know where to sync from.
In order to achive this `gitlab-mirror` expects the description field of a mirrored project to
be valid [YAML](http://yaml.org/) with at least an `origin` field.

``` yaml
origin: https://git.example.org/my-project.git
```

A list of currently supported fields

- `origin` Source repository to mirror from
- `skip`   Temporarily exclude a project from syncing by adding `skip: true`
- `destination` Reserved for future use

Any other fields are ignored

### Building & Installing

In order to build this project you need a least rust v1.18.0. The easiest way to get rust is via: [rustup.rs](http://rustup.rs/)

The project can be built using cargo

```
cargo build
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details
