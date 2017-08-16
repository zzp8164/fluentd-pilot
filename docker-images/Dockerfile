FROM ruby:2.3

RUN apt-get update && \
  apt-get install git -y &&\
  apt-get install wget -y &&\
  apt-get install ruby-dev -y &&\
  gem install fluentd -v "~> 0.12.0" --no-ri --no-rdoc && \
  gem install fluent-plugin-elasticsearch --no-ri --no-rdoc && \
  gem install gelf -v "~> 3.0.0" --no-ri --no-rdoc && \
  gem install aliyun_sls_sdk -v ">=0.0.9" --no-ri --no-rdoc && \
  gem install specific_install --no-ri --no-rdoc&& \
  gem specific_install https://github.com/RussellCloud/fluent-plugin-kafka.git && \
  gem install zookeeper --no-ri --no-rdoc&& \
  gem install ruby-kafka --no-ri --no-rdoc&& \
  rm -rf /root/.gem

COPY plugins/ /etc/fluentd/plugins/

VOLUME /etc/fluentd/conf.d

COPY pilot fluentd.tpl entrypoint config.default /pilot/
VOLUME /pilot/pos

EXPOSE 24224
WORKDIR /pilot/
#CMD exec fluentd -c /fluentd/etc/$FLUENTD_CONF -p /fluentd/plugins $FLUENTD_OPT
CMD /pilot/entrypoint
