FROM fluent/fluentd:v0.14-debian-onbuild

# below RUN includes plugin as examples elasticsearch is not required
# you may customize including plugins as you wish

RUN buildDeps="sudo make gcc g++ libc-dev ruby-dev" \
 && apt-get update \
 && apt-get install -y --no-install-recommends $buildDeps \
                    curl \
                    net-tools \
 && sudo gem install \
        fluent-plugin-influxdb:1.0.0.rc3 \
        fluent-plugin-rewrite-tag-filter \
        fluent-plugin-filter_typecast \
        fluent-mixin-config-placeholders \
        fluent-plugin-record_splitter \
        --no-document \
 && sudo gem sources --clear-all \
 && SUDO_FORCE_REMOVE=yes \
    apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
 && rm -rf /var/lib/apt/lists/* \
           /home/fluent/.gem/ruby/2.3.0/cache/*.gem