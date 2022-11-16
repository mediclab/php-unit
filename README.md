# PHP Nginx-Unit Docker Image

Nginx Unit with PHP Docker container builded for ARM64 and AMD64 architectures

### Using:
Builded on official Nginx Unit images. You can find documentation on: https://unit.nginx.org/installation/#docker-images

### Available tags:
* medic84/php-unit:latest
* medic84/php-unit:php8.1
* medic84/php-unit:php8.1-unit1.28.0
* medic84/php-unit:php8.0
* medic84/php-unit:php8.0-unit1.28.0
* medic84/php-unit:php7.4
* medic84/php-unit:php7.4-unit1.28.0

### Example:

Laravel config:
```json
{
    "listeners": {
        "*:80": {
            "pass": "routes"
        }
    },
    "routes": [
        {
            "match": {
                "uri": [
                    "*.php",
                    "*.php/*"
                ]
            },

            "action": {
                "pass": "applications/laravel/direct"
            }
        },
        {
            "action": {
                "share": "/var/www/public/$uri",
                "fallback": {
                    "pass": "applications/laravel/index"
                }
            }
        }
    ],
    "applications": {
        "laravel": {
            "type": "php",
            "processes": 5,
            "user": "user",
            "group": "user",
            "targets": {
                "direct": {
                    "root": "/var/www/public/"
                },

                "index": {
                    "root": "/var/www/public/",
                    "script": "index.php"
                }
            }
        }
    }
}
```