FROM postgres:9.6
MAINTAINER Andreas Mueller <andreas@kwiqly.com>
ENV PLV8XDB test
RUN echo 'deb http://cran.rstudio.com/bin/linux/debian jessie-cran3/' >>/etc/apt/sources.list
 

RUN apt-get update \
	&& apt-get install -y --force-yes  liblapack-dev build-essential libv8-dev git-core postgresql-server-dev-$PG_MAJOR postgresql-$PG_MAJOR-plr libcurl4-gnutls-dev\
	&& rm -rf /var/lib/apt/lists/*
 
RUN R -e "install.packages(c('curl','ineq','dplyr', 'git2r', 'tidyr', 'readr', 'ineq', 'cobs', 'reshape2', 'httr', 'devtools', 'scales'), repos='https://cran.rstudio.com/')"

ENV PLV8_BRANCH r1.4


RUN cd /tmp && git clone -b $PLV8_BRANCH https://github.com/plv8/plv8.git \
  && cd /tmp/plv8 \
  && make all install

RUN echo "plv8.start_proc = 'plv8_startup'">>/var/lib/postgresql/data/postgresql.conf
 
