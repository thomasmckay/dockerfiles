FROM centos:7

COPY hammer.repo /etc/yum.repos.d/hammer.repo
RUN yum -y install foreman-release-scl
RUN yum -y install http://cbs.centos.org/kojifiles/packages/centos-release-scl/1/1.el7.centos/noarch/centos-release-scl-1-1.el7.centos.noarch.rpm
RUN yum clean all && yum repolist && yum update -y
RUN yum -y install \
    foreman-release-scl \
    tfm-rubygem-hammer_cli \
    tfm-rubygem-hammer_cli_katello

# hammer-cli-csv
RUN yum -y install git
RUN yum -y install libstdc++-devel make gcc-c++ ruby-devel rubygems rubygem-bundler
RUN gem install --no-rdoc --no-ri hammer_cli_katello

RUN git clone https://github.com/Katello/hammer-cli-katello.git
RUN cd hammer-cli-katello && gem build hammer_cli_katello.gemspec && gem install --no-rdoc --no-ri hammer_cli_katello
RUN echo ":katello:" > /etc/hammer/cli.modules.d/katello.yml
RUN echo "  :enable_module: true" >> /etc/hammer/cli.modules.d/katello.yml

RUN git clone https://github.com/Katello/hammer-cli-csv.git
RUN cd hammer-cli-csv && gem build hammer_cli_csv.gemspec && gem install --no-rdoc --no-ri hammer_cli_csv
RUN echo ":csv:" > /etc/hammer/cli.modules.d/csv.yml
RUN echo "  :enable_module: true" >> /etc/hammer/cli.modules.d/csv.yml

RUN cd

CMD hammer
