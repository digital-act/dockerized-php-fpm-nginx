Dockerized php-fpm with nginx.

## Steps

1) Clone

2) Duplicate docker-compose.override.yml.dist without .dist part & make required adjustments if needed.

3) Symlink or copy software to project directory. (default nginx root points to public folder, which is fine for laravel)

4) `docker-compose up -d` to spin up containers.