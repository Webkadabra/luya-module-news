Start collaboration
===================

How to collaborate with us and contribute to the LUYA Project.

1. Fork Luya
2. Recommended directory structure
3. Clone luya fork
4. Create luya-kickstarter project
4.1. Update config
4.2. Update composer.json
5. Define the upstream repo
6. Work routine
7. Add changes to zephir/luya (Pull request)

1. Fork Luya
-------------
Fork the Luya project on Github: [https://github.com/zephir/luya](https://github.com/zephir/luya).
![fork-luya](img/start-collaboration-fork.jpg "Fork Luya")

2. Recommended directory structure
------------------------------------
You will have two directories that depends on each other.

1. The «luya» directory
2. The «luya-kickstarter» directory

I will work with the following structure:
```
luya/
├ luya/     # luya
├ website/  # luya-kickstarter
```

3. Clone luya fork
-------------------
Working directory: luya/luya/

Use following command to clone the forked Luya project.

Don't forget to replace "username" with your Github username
```
git clone https://github.com/username/luya.git .
```

Install Luya. For the complete guide, visit: [https://github.com/zephir/luya](https://github.com/zephir/luya)

4. Create luya-kickstarter project
------------------------------------
Working directory: luya/website/

1. Create the luya-kickstarter project with composer.
2. Move all files from the created directory into luya/website/
```
composer create-project zephir/luya-kickstarter:dev-master
```
You will be asked if you want to remove the .git files. Answer with Y if you want to push the luya-kickstarter project into your own repository.
```
Do you want to remove the existing VCS (.git, .svn..) history? [Y,n]? 
```
Now you have to move all files to your main folder.
```
mv luya-kickstarter/* . && mv luya-kickstarter/.* .
rm -rf luya-kickstarter/
```
All files are now in the right place.

### 4.1 Updated config
Copy local config template:
```
cp config/local.php.dist config/local.php
```
Edit local config and update db informations:
```
'db' => [
	'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=localhost;dbname=your_dbname;unix_socket=your_unix_socket',
    'username' => 'your_username',
    'password' => 'your_password'
]
```

### 4.2 Updated composer
To work on luya modules, we have to update the composer.json.
Change it's content to the following:
```
{
    ...
    "require": {
        "yiisoft/yii2": "2.0.*"
    },
    ...
    "autoload" : {
        "psr-4" : {
            "luya\\" : "../luya/src/",
            "admin\\" : "../luya/modules/admin",
            "cms\\" : "../luya/modules/cms",
            "cmsadmin\\" : "../luya/modules/cmsadmin"
        }
    },
    ...
}
```
**Run:**
```
composer update
```

All luya relevant files are now loaded from the luya/luya/ folder.

For more informations and troubleshooting: https://github.com/zephir/luya-kickstarter

Working (sh) ***@TBD***
-------------
```
chmod +x rebasemaster.sh
```

firsttime
```
./rebasemaster.sh init
```

else
```
./rebasemaster.sh
```


Define the upstream repo
-------------------------
Working directory: luya/luya/

To update your fork you have to add the original repo:
```
git remote add upstream https://github.com/zephir/luya.git
```

Working routine
----------------
Before working on luya, you have to update your local master branch to the newest version:
```
git checkout master
git fetch upstream
git rebase upstream/master
```


Now that you're on the newest release, create a branch from master:
Don't forget to replace "newBranch" with a meaningful name.
```
git checkout -b newBranch master
```

Commit & Push all changes to this new branch.

Add changes to zephir/luya (Pull request)
-----------------------------------------
Now that you've committed and pushed all of your files, go to your forked luya project on Github.
Click on «Pull request» on the right side and then on the green button «New pull request».

On the following screen, choose your branch to merge, check everything and create the pull request.
![pull-request](img/start-collaboration-pull-request.jpg "Pull request")