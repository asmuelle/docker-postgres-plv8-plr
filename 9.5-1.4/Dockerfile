FROM postgres:9.5
MAINTAINER Andreas Mueller <andreas@kwiqly.com>
ENV PLV8XDB test
RUN echo 'deb http://cran.rstudio.com/bin/linux/debian jessie-cran3/' >>/etc/apt/sources.list
 

RUN apt-get update \
	&& apt-get install -y --force-yes build-essential libv8-dev git-core postgresql-server-dev-$PG_MAJOR postgresql-$PG_MAJOR-plr\
	&& rm -rf /var/lib/apt/lists/*
 
RUN R -e "install.packages(c('ineq','dplyr'), repos='https://cran.rstudio.com/')"
RUN R -e 'if(!require("devtools")) install.packages("devtools",  repos="http://140.107.3.21")'


RUN R -e 'if(!require("git2r")) install.packages("git2r",  repos="http://140.107.3.21")'
 
RUN R -e 'if(!require("tidyr")) install.packages("tidyr",  repos="http://140.107.3.21")'
RUN R -e 'if(!require("readr")) install.packages("readr",  repos="http://140.107.3.21")'
RUN R -e 'if(!require("ineq")) install.packages("ineq",  repos="http://140.107.3.21")'
RUN R -e 'if(!require("reshape2")) install.packages("reshape2",  repos="http://140.107.3.21")'
ENV PLV8_BRANCH r1.4


RUN cd /tmp && git clone -b $PLV8_BRANCH https://github.com/plv8/plv8.git \
  && cd /tmp/plv8 \
  && make all install

RUN echo "plv8.start_proc = 'plv8_startup'">>/var/lib/postgresql/data/postgresql.conf
 
