# DO NOT EDIT FILES CALLED 'Dockerfile'; they are automatically
# generated. Edit 'Dockerfile.in' and generate the 'Dockerfile'
# with the 'rake' command.

# The suggested name for this image is: bioconductor/release_base.

FROM rocker/rstudio:3.5.3

# FIXME? in release, default CRAN mirror is set to rstudio....should it be fhcrc?

MAINTAINER maintainer@bioconductor.org

# nuke cache dirs before installing pkgs; tip from Dirk E fixes broken img
RUN  rm -f /var/lib/dpkg/available && rm -rf  /var/cache/apt/*


# temporarily (?) change mirror used
# RUN sed -i.bak 's!http://httpredir.debian.org/debian jessie main!http://mirrors.kernel.org/debian jessie main!' /etc/apt/sources.list

# temporarily (?) remove explicit jessie source
#RUN sed -i.bak -e '/deb http:..ftp.de.debian.org.debian jessie main/d' /etc/apt/sources.list

# currently unstable option not available



RUN apt-get update && \
    apt-get -y  install --fix-missing gdb libxml2-dev python-pip libz-dev libmariadb-client-lgpl-dev
    # valgrind


RUN pip install awscli




# requested install 
RUN apt-get update && apt-get -y install libpng-dev

# install headers needed for Rhtslib
RUN apt-get update && apt-get -y install libbz2-dev liblzma-dev



ADD install.R /tmp/

RUN R -f /tmp/install.R

RUN echo "R_LIBS=/usr/local/lib/R/host-site-library:\${R_LIBS}" > /usr/local/lib/R/etc/Renviron.site
RUN echo "R_LIBS_USER=''" >> /usr/local/lib/R/etc/Renviron.site
RUN echo "options(defaultPackages=c(getOption('defaultPackages'),'BiocManager'))" >> /usr/local/lib/R/etc/Rprofile.site

