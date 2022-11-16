# PHP Nginx-Unit Docker Image

Nginx Unit with PHP Docker container builded for ARM64 and AMD64 architectures

### Using:
Builded on official Nginx Unit images. You can find documentation on: https://unit.nginx.org/installation/#docker-images

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