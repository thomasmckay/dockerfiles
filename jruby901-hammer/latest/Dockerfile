FROM jruby:9.0.1

RUN mkdir /etc/hammer
COPY cli_config.yml /etc/hammer/cli_config.yml
RUN gem install hammer_cli_katello

# hammer-cli-csv
RUN wget https://github.com/Katello/hammer-cli-csv/archive/master.zip && unzip master.zip
RUN cd hammer-cli-csv-master && gem build hammer_cli_csv.gemspec && gem install --no-rdoc --no-ri ./hammer_cli_csv-*.gem


CMD hammer