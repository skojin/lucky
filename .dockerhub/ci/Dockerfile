FROM crystallang/crystal:0.35.1 as builder

WORKDIR /data

RUN git clone https://github.com/luckyframework/lucky_cli && cd lucky_cli && git checkout v0.24.0 && \
  shards install && crystal build src/lucky.cr

RUN ./lucky_cli/lucky -v

FROM crystallang/crystal:0.35.1

RUN apt-get update && \
  apt-get install -y libpq-dev postgresql-client chromium-chromedriver git && \
  # Cleanup leftovers
  apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY --from=builder /data/lucky_cli/lucky /usr/local/bin/lucky

