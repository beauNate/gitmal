<p align="center"><img src="img/gitmal-color-logo.webp" alt="Gitmal" width="330" height="330"></p>

# Gitmal

Gitmal is a static page generator for Git repositories. Gitmal generates static HTML pages with files, commits,
code highlighting, and markdown rendering.

## Installation

```sh
go install github.com/antonmedv/gitmal@latest
```

```sh
docker run --rm -v $(pwd):/repo antonmedv/gitmal /repo
```

## Usage

Run gitmal in the repository dir. Gitmal will generate pages in _./output_ directory.

```sh
gitmal .
```

Run gitmal with `--help` flag, go get a list of available options.

```sh
gitmal --help
```

## Screenshots

<p align="center">
  <a href="img/gitmal-screenshot-code-highlighting.webp"><img src="img/gitmal-screenshot-code-highlighting.webp" alt="Gitmal Code Highlighting" width="400"></a>
  <a href="img/gitmal-screenshot-file-tree.webp"><img src="img/gitmal-screenshot-file-tree.webp" alt="Gitmal File Tree" width="400"></a><br>
  <a href="img/gitmal-screenshot-files.webp"><img src="img/gitmal-screenshot-files.webp" alt="Gitmal Files Page" width="400"></a>
</p>

## Examples

Here are a few examples of repos hosted on my website:

- [git.medv.io/zx/](https://git.medv.io/zx/) — github.com/google/zx
- [git.medv.io/zig/](https://git.medv.io/zig/) — codeberg.org/ziglang/zig (light theme)
- [git.medv.io/my-badges/](https://git.medv.io/my-badges/) — github.com/my-badges/my-badges

Gitmal on kubernetes repository works as well. Generation on my MacBook Air M2 with `--minify` and `--gzip` flags
takes around 25 minutes, and the generated files weigh around 2 GB.

## Themes

Gitmal supports different code highlighting themes. You can customize the theme with `--theme` flag.

```sh
gitmal --theme github-dark
```

## Auto‑updates

You can automatically regenerate the static files every time you push to a repository by using a `post-receive` hook.

1. **Create a bare repository**

   ```sh
   git init --bare ~/myrepo.git
   ```

   Add it as a remote and push:

   ```sh
   git remote add origin user@server:~/myrepo.git
   ```

2. **Add the post‑receive hook**

   Create `~/myrepo.git/hooks/post-receive` with the following contents and make it executable:

   ```sh
   #!/bin/sh
   
   NO_OUTPUT_DIR_CHECK=1 /path-to/gitmal --output /var/www/myrepo
   ```

   And make it executable:

   ```sh
   chmod +x ~/myrepo.git/hooks/post-receive
   ```

   Now, every `git push` will trigger a rebuild.

## License

[MIT](LICENSE)
