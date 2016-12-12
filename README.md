# LUYA News Module

The news module will provided you a basic news system with categories and tags.

## Installation

In order to install the news module you have to require the `luyadev/luya-module-news`. To add the modules to your composer run:

```sh
composer require luyadev/luya-module-news:^1.0@dev
```

This will add the packages to your composer.json and run the update command. So now you have the modules in your vendor folder. Now you have the configure them in your configration (the `configs` folder) file:

```php
'news' => 'luya\news\frontend\Module',
'newsadmin' => 'luya\news\admin\Module',
```

The modules are now available in your project. Now you have to run the migration and import command and you will be able to access the news administration to add news articles.

migration command:

```sh
./vendor/bin/luya migrate
```

and import command:

```sh
./vendor/bin/luya import
```

After adding the persmissions to your group you will be able to edit and add new news articles.

## Example Views

As the module will try to render a view for the news overview, here is what this could look like this in a very basic way:

#### views/news/default/index.php

```php
<?php foreach($provider->getModels()->all() as $item): ?>
    <?php /* @var $item \luya\news\models\Article */ ?>
    <pre>
        <?php print_r($item->toArray()); ?>
    </pre>
    <p>
        <a href="<?= $item->getDetailUrl(); ?>">News Detail Link</a>
    </p>
<?php endforeach; ?>

<?= \yii\widgets\LinkPager::widget(['pagination' => $provider->pagination]); ?>
```

#### views/news/default/detail.php

```php
<pre>
<?php print_r($model->toArray()); ?>
</pre>
```

The above examples will just dump all the data from the model active records.