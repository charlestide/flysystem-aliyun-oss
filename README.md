# Flysystem Adapter for Aliyun OSS 
> Forked From apollopy/flysystem-aliyun-oss

This is a Flysystem adapter that forked from [apollopy/flysystem-aliyun-oss](https://github.com/apollopy/flysystem-aliyun-oss)

Changes:
* Add isCName Configure, Now Configuration has new option named "is_cname"
* Add SSL Configure, Now the ssl option specify whether use ssl
```php
        'oss' => [
            'driver'     => 'oss',
            'access_id'  => env('OSS_ACCESS_ID','your id'),
            'access_key' => env('OSS_ACCESS_KEY','your key'),
            'bucket'     => env('OSS_BUCKET','your bucket'),
            'endpoint'   => env('OSS_ENDPOINT','your endpoint'),
            'is_cname'   => env('OSS_IS_CNAME','is_cname'),
            'prefix'     => env('OSS_PREFIX', ''), // optional
            'ssl'        => env('OSS_SSL', false)
        ],
```
* Add getUrl Method to Class AliyunOssAdapter, so you can use follow method
* Upgrade aliyuncs/oss-sdk-php version from ~2.2.1 to >=2.0
```php
$url = Storage::cloud()->url($path);
``` 

# Original Readme

## Installation

```bash
composer require apollopy/flysystem-aliyun-oss
```

## for Laravel

This service provider must be registered.

```php
// config/app.php

'providers' => [
    '...',
    ApolloPY\Flysystem\AliyunOss\AliyunOssServiceProvider::class,
];
```

edit the config file: config/filesystems.php

add config

```php
'oss' => [
    'driver'     => 'oss',
    'access_id'  => env('OSS_ACCESS_ID','your id'),
    'access_key' => env('OSS_ACCESS_KEY','your key'),
    'bucket'     => env('OSS_BUCKET','your bucket'),
    'endpoint'   => env('OSS_ENDPOINT','your endpoint'),
    'prefix'     => env('OSS_PREFIX', ''), // optional
],
```

change default to oss

```php
    'default' => 'oss'
```

## Use

see [Laravel wiki](https://laravel.com/docs/5.1/filesystem)

## Plugins

inspire by [itbdw/laravel-storage-qiniu](https://github.com/itbdw/laravel-storage-qiniu)

```php
Storage::disk('oss')->putFile($md5_path, '/local_file_path/1.png', ['mimetype' => 'image/png','filename' => 'filename_by_down.png']);

Storage::disk('oss')->signedDownloadUrl($path, 3600, 'oss-cn-beijing.aliyuncs.com', true);
```

## IDE Helper

if installed [barryvdh/laravel-ide-helper](https://github.com/barryvdh/laravel-ide-helper)

edit the config file: config/ide-helper.php

```php
'interfaces'      => [
    '\Illuminate\Contracts\Filesystem\Filesystem' => ApolloPY\Flysystem\AliyunOss\FilesystemAdapter::class,
],
```
