MDPIAssetBundle
===================

In order to get rid of the global assets version in Symfony2.<br>
The bundle provide a command "mdpi:assets:versions" to generate a list of assets with its unique version numbers, which then can be used by the twig helper function "asset()"

Install
-------

1. add the bundle into your deps:
```
[MDPIAssetBundle]
    git=git@git://github.com/mdpi/MDPIAssetBundle.git
    version=origin/master
    target=/bundles/MDPI/AssetBundle
```

2. run "bin/vendors install"

3. update your app/autoload.php
```php
<?php
// ...
$loader->registerNamespaces(array(
    'Symfony'          => array(__DIR__.'/../vendor/symfony/src', __DIR__.'/../vendor/bundles'),
    // ...
    'MDPI'             => __DIR__.'/../vendor/bundles',
));
// ...
?>
```

4. update your app/AppKernel.php
```php
<?php
// ...
public function registerBundles()
    {
        $bundles = array(
            new Symfony\Bundle\DoctrineFixturesBundle\DoctrineFixturesBundle(),
            // ...
            new MDPI\AssetBundle\MDPIAssetBundle(),
        );
// ...
?>
```

5. remove the global assets version from your config file if it's used.

6. import the services.yml file into your config file
```
imports:
    - { resource: parameters.ini }
    # ....
    - { resource: @MDPIAssetBundle/Resources/config/services.yml }
```

Example: Generate assets versions (in production environment usually)
------------------------

```
$ app/console help mdpi:assets:versions  # show help message

# generate for all of bundles
$ app/console -e=prod mdpi:assets:versions

# generate all but don't include bundlename in generated filenames
$ app/console -e=prod mdpi:assets:versions --trim-bundlename=yes

# generate only for a specified bundle (MDPIMainBundle here)
$ app/console -e=prod mdpi:assets:versions MDPIMain 
```
