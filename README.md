# ddev-pull-backwpupfile

This providers script will import a backup file created with [BackWPup – WordPress Backup Plugin](https://wordpress.org/plugins/backwpup/) (Open Source) into a DDEV project.

*This is an unofficial community script. Thanks you, Inpsyde GmbH, for providing BackWPup as Open Source!*

**Features:**

- Imports database and files from a backwpup .zip-backup
- This providers script will automatically replace (migrate) the URLs in database
- The files import only overrides files which are not tracked by git (using the .gitignore file, see example of wp-content/themes/twenty-twenty-childtheme). This allows you to manage child themes or custom plugins in your git project (and push them to your live site via [git-updater](https://git-updater.com/) or [wppusher](https://wppusher.com/)).

## Use it

1. Clone this repository to your local harddrive
1. Setup your project with `ddev config --project-type=wordpress`
1. `ddev start`

### Import a backup 
1. Create a zip-backup of your site with [BackWPup – WordPress Backup Plugin](https://wordpress.org/plugins/backwpup/)
1. Download the backup file to this project folder
1. Rename the .zip file to `backup.zip`
1. `ddev pull backwpupfile`
1. `ddev launch`

## Technical background

See [DDEV providers](https://ddev.readthedocs.io/en/stable/users/providers/provider-introduction/) for more information about providers integration. The magic is happening in `.ddev/providers/backwpupfile.yaml`. 

## TODOs

- [ ] check if git-tracked child theme is really not overriden by import, upload & install child theme on live site

Screencast: coming soon

## See as well:

- https://matthias-andrasch.eu/blog/2021/ddev-wordpress-cli-clone-a-live-site-to-your-local-laptop/
- https://ddev.readthedocs.io/en/stable/users/providers/provider-introduction/