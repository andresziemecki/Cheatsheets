# Make curl request and save json body response

``` bash
curl --location 'https://api.tequila.kiwi.com/locations/dump?locale=en-US&location_types=airport&limit=10000&sort=name&active_only=true' \
--header 'accept: application/json' \
--header 'apikey: uwz9tsLG8onWXy8bSBJzeXZrSGGQxzRN'  -o out.json
```