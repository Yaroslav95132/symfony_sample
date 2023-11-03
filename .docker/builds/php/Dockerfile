FROM php:8.2-fpm

ENV user dev
ARG PUID=1000
ARG PGID=1000
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/
# Install composer
COPY --from=composer:2.4 /usr/bin/composer /usr/bin/
ENV COMPOSER_ALLOW_SUPERUSER=1
ENV PATH="./vendor/bin:$PATH"

RUN groupadd -g $PGID $user \
  && useradd -u $PUID -g $user -m $user \
  && apt-get update && apt-get install -y --no-install-recommends \
      git \
      curl \
      libpng-dev \
      libonig-dev \
      libxml2-dev \
      zip \
      unzip

# Install PHP extensions
RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

USER $user

CMD ["php-fpm"]
