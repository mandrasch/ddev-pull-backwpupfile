# ddev-pull-backwpupfile

This providers script will import a backup file created with [BackWPup – WordPress Backup Plugin](https://wordpress.org/plugins/backwpup/) (Open Source) into a DDEV project.

*This is an unofficial community script. Thanks you, Inpsyde GmbH, for providing BackWPup as Open Source!*

**Features:**

- This [DDEV providers](https://github.com/mandrasch/ddev-pull-backwpupfile/blob/main/.ddev/providers/backwpupfile.yaml)  script imports database and files from a backwpup .zip-backup
- The script will automatically replace (migrate) the URLs in database
- The files import only overrides files which are not tracked by git (using the .gitignore file, see example of wp-content/themes/twentytwentyone-child). This allows you to manage child themes or custom plugins in your git project (and push them to your live site via [git-updater](https://git-updater.com/) or [wppusher](https://wppusher.com/)).
- Works without SSH access to your webspace (If you have SSH access with rsync and mysqldump available, you can use a more efficient workflow and sync only new files. See [rsync.yaml.example](https://github.com/drud/ddev/blob/master/pkg/ddevapp/dotddev_assets/providers/rsync.yaml.example), but it needs adaption for WordPress)

## Use it

1. Fork this repository via "Use this template"-button
1. Clone to your local harddrive
1. Setup your project with `ddev config --project-type=wordpress`
1. `ddev start`

### Import a backup 
1. Create a zip-backup of your site with [BackWPup – WordPress Backup Plugin](https://wordpress.org/plugins/backwpup/)
1. Download the backup file to this project folder
1. Rename the .zip file to `backup.zip`
1. `ddev start`
1. `ddev pull backwpupfile`
1. `ddev launch`

Screencast: coming soon, see blog post with screenshots: https://matthias-andrasch.eu/blog/2021/import-a-wordpress-site-into-ddev-ddev-pull-backwpupfile/

## Technical background

See [DDEV providers](https://ddev.readthedocs.io/en/stable/users/providers/provider-introduction/) for more information about providers integration. The magic is happening in [`.ddev/providers/backwpupfile.yaml`](https://github.com/mandrasch/ddev-pull-backwpupfile/blob/main/.ddev/providers/backwpupfile.yaml). 

## Reset

Remove all changes and reset everything, only git tracked files will be left.

```
ddev delete -O
git clean -fdx
```

(You need to run `ddev config --project-type=wordpress` again if you haven't added .ddev/config.yaml to git.)

## TODOs

- [ ] check if git-tracked child theme is really not overriden by import, upload & install child theme on live site
- [ ] refresh permalinks structure if we switch from apache to nginx and vice versa? 
- [ ] Test with subdirectory as docroot
- [ ] Test with multiple zip files (large backups)

## See as well:

- https://matthias-andrasch.eu/blog/2021/ddev-wordpress-cli-clone-a-live-site-to-your-local-laptop/
- https://ddev.readthedocs.io/en/stable/users/providers/provider-introduction/
- Old project: https://github.com/mandrasch/ddev-wp-groundstation
