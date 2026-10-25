# CanvasCore template library

Starter pages, sections and full-site kits for [CanvasCore](https://github.com/sputlab/canvascore), shared by the community.
CanvasCore sites list them under **Administration › Template library** and install them with one click.

- `index.json` + `index.json.sig`: the list of kits, **signed** by the CanvasCore maintainers. Sites only trust an index whose signature verifies.
- `<id>-<version>.zip`: one kit each; `<id>-preview.png`: its picture in the library.

## What is a kit

A ZIP with `kit.json` (id, name, version, type `page` | `section` | `site`, author, description, license, tags, minVersion), `content.json`
(the page, sections or site), an optional `preview.png`, and the images its blocks use in `assets/` (written `kit:assets/<file>` in the content).
A kit holds **no code**: Custom HTML, form addresses and custom CSS/JavaScript are dropped when a site installs it, and everything else is
cleaned like an editor's save. The format is described in section 8.4 of the
[Developer Guide](https://github.com/sputlab/canvascore/blob/main/docs/manuals/DEVELOPER-GUIDE.md).

## Share a kit

1. Make the folder of your kit (start from `docs/examples/library-kits` in the CanvasCore repository).
2. Check it: `php canvascore-frontend/scripts/library-kit.php check <folder>`, and pack it: `… pack <folder>`.
3. Open a pull request here with the ZIP. By sending it you license the kit under the license you put in `kit.json` (CC0-1.0 or another permissive
   license is welcome) and confirm that the content and images are yours to share.

## For the maintainers: publishing

After merging kits, rebuild and sign the index with the release key, then commit the result:

```bash
php canvascore-frontend/scripts/library-index.php --key=$HOME/.canvascore/release-signing.key \
  --kits=<this folder> --base-url=https://raw.githubusercontent.com/sputlab/canvascore-library/main/ --out=<this folder>
```

The index is checked against the public keys in `canvascore-admin/update-keys.php`, so only a maintainer's key produces an index sites accept.
The three kits here are the examples of the CanvasCore repository (license CC0-1.0).
