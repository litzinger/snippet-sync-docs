---
title: Snippet Sync
taxonomy:
    category: docs
---

>>> Snippet Sync is only a 1 way sync. It will take files and create database entries from them. It will not sync existing snippets from the database to flat files.

>>> Snippet Sync will only sync a snippet if you are logged in as a Super Admin user, or have your $config[‘debug’] value set to 1 or 2. This way the extra overhead of comparing the snippet’s file contents and updating the database will not happen on every page load on a production site.

By default Snippet Sync will look for your snippet files within the /system/expressionengine/snippets folder, however, there is a $config variable to change this path.

```
$config['snippet_file_basepath'] = '/my/path/';
```

You can also set your snippet prefix as a config variable too.

```
$config['snippets_sync_prefix'] = 'snippet:';
```

If you use the default prefix of snippet: then you will not be able to edit and save the snippet within the EE control panel. It does not allow semi-colons in snippet names, but this may defeat the purpose of Snippet Sync entirely as it was intended to move the editing process of snippets to the file system and out of the control panel.

You can optionally choose to organize your snippets into separate folders for each site and sub-folders, just like you do templates. For example: ``/snippets/default_site/my_snippet.html`` - Will be used in your template as ``{snippet:my_snippet}``

OR

``/snippets/default_site/global.group/header.html`` - Will be used in your template as ``{snippet:global_header}``

Sub-folders can optionally be suffixed with a separator. By default it is set to an underscore. In the example above, the suffix is the underscore between global and header. There is a config override value for this as well:

```
$config['snippets_sync_suffix'] = '_';
```

If you are using MSM and want to share snippets between all the sites you can create a “shared” folder in the root of your snippets folder. By default it is named shared, but you can change it to whatever you want in the extension settings page. You can also set this value with the following config value.

```
$config['msm_shared_folder'] = 'shared';
```

Once you setup the configuration options your snippets folder may resemble this structure.

```
snippets/
-- default_site/
---- global/
------ header.html
---- products/
------ detail.html
------ list.html
-- site_two/
---- global/
------ header.html
-- shared/
---- global/
------ footer.html
```

The following variables will be created based on directory structure above.

Available in your first (default site).

```
{snippet:global_header}
{snippet:products_detail}
{snippet:products_list}
{snippet:shared_global_footer}
```

Available in your second site.

```
{snippet:global_header}
{snippet:shared_global_footer}
```