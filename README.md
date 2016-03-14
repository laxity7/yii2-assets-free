# [cebe/assetfree-yii2](https://packagist.org/packages/cebe/assetfree-yii2) composer package

A composer package that allows you to install [yii2](https://github.com/yiisoft/yii2) without [composer-asset-plugin](https://github.com/francoispluchino/composer-asset-plugin).

## How to use?

Just require `cebe/assetfree-yii2` instead of `yiisoft/yii2` in your `composer.json`.

## Why?

Yii2 currently depends on Asset packages to make it really easy to create frontend applications as it directly provides Widgets and Javascript/CSS components out of the box. Therefore, the [composer-asset-plugin](https://github.com/francoispluchino/composer-asset-plugin) is used which allows to
manage frontend dependencies directly in composer.json.

Sometimes however, these frontend components are not needed, e.g. if you use Yii to create a Console Application, Background workers or a REST API. So if you do not want to install the composer-asset-plugin on your production servers because you
do not need any asset functionality anyway you may use this package instead of requiring `yiisoft/yii2` directly.

## How does this work?

Magic: https://github.com/cebe/assetfree-yii2/blob/2.0.0/composer.json#L9-L14 :)

This package claims to "[provide](https://getcomposer.org/doc/04-schema.md#provide)" the required asset packages which are only
available when composer-asset-plugin ist installed. In reallity no asset packages are installed, so this is only useful in cases [where you do not need them](#why).

### Caution!

While this will work without known issues, when composer-asset-plugin is not installed, you may get in trouble if you run this with the plugin enabled. If the composer-asset-plugin is installed the required packages will get installed and you may not be able to deploy your `composer.lock`, which has been created in this situation, to production.

So either make sure the plugin is not installed, or run composer with `--no-plugins` switch.

If you acidentally ran composer install or update with the plugin the only way to fix it is to delete composer.lock and vendor dir and install again.

