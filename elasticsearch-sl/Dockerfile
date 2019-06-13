FROM elasticsearch:7.1.1

ENV ELASTICSEARCH_VERSION 7.1.1

# install the lemmagen plugin and download the slovenian lexicon
RUN ./bin/elasticsearch-plugin install https://github.com/vhyza/elasticsearch-analysis-lemmagen/releases/download/v$ELASTICSEARCH_VERSION/elasticsearch-analysis-lemmagen-$ELASTICSEARCH_VERSION-plugin.zip --batch \
    && curl -L -O https://github.com/vhyza/lemmagen-lexicons/raw/master/free/lexicons/sl.lem \
    && mkdir config/lemmagen \
    && mv sl.lem config/lemmagen
