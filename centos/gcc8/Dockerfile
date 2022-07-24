FROM centos:centos7.9.2009

RUN  set -eux; \
     yum install -y gcc gcc-c++ vim kde-l10n-Chinese bison gettext \
         texinfo make autotool automake \
	 wget curl zip unzip bzip2 file sudo readline ncurses which \
	 git net-tools python3-devel python3 python3-pipi \ 
         wqy-microhei-fonts bash-completion \
         man-db man-pages-zh-CN man-pages; \
     localedef -i zh_CN -f UTF-8 zh_CN.utf8; \
     localedef -i en_US -f UTF-8 en_US.utf8; \
     useradd -m -s /bin/bash -r finance; \
     echo "finance:123456"|chpasswd; \ 
     echo "finance ALL=(ALL) ALL" >> /etc/sudoers; \
     ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime; \
     echo ":set encoding=utf8" >> /etc/vimrc; \
     yum clean all; \
     rm -rf /var/cache/yum/* ; \
     rm -rf /var/lib/rpm/__db.* ; \ 
     rm -rf /var/lib/yum/* ; \
     mkdir -p /packages && cd /packages; \
     wget --no-check-certificate  https://mirror.tuna.tsinghua.edu.cn/gnu/make/make-4.2.1.tar.gz; \
     tar -xf make-4.2.1.tar.gz && rm -rf make-4.2.1.tar.gz && cd make-4.2.1; \
     mkdir build && cd build; \
     ../configure --prefix=/usr;\
     make && make install;\
     cd /packages && rm -rf /packages/make-4.2.1; \
     wget --no-check-certificate https://mirror.tuna.tsinghua.edu.cn/gnu/gcc/gcc-8.5.0/gcc-8.5.0.tar.xz;\
     tar -xf gcc-8.5.0.tar.xz  && rm -rf gcc-8.5.0.tar.xz && cd gcc-8.5.0;\
     ./contrib/download_prerequisites;\
     mkdir build && cd build;\
     ../configure --enable-bootstrap --enable-languages=c,c++,fortran,lto \
         --prefix=/usr --enable-shared --enable-threads=posix --enable-checking=release \
         --disable-multilib --enable-__cxa_atexit --disable-libunwind-exceptions \
         --enable-gnu-unique-object --enable-linker-build-id  --with-linker-hash-style=gnu \
         --enable-plugin --enable-initfini-array -enable-gnu-indirect-function  \
         --with-tune=generic --with-arch_32=x86-64 --build=x86_64-redhat-linux;\
      make -j 8 && make install-strip;\
      cd /packages && rm -rf /packages/gcc-8.4.0; \
      wget --no-check-certificate https://mirror.tuna.tsinghua.edu.cn/gnu/glibc/glibc-2.28.tar.xz; \
      tar -xf glibc-2.28.tar.xz && rm -rf glibc-2.28.tar.xz && cd glibc-2.28; \
      mkdir build && cd build; \
      sed -i 's/$name ne "nss_test1"/$name ne "nss_test1" \&\& $name ne "nss_test2"/' ../scripts/test-installation.pl;\
      ../configure --prefix=/usr --enable-obsolete-nsl;\
      make -j 8 && make install;\
      cd /packages && rm -rf /packages/glibc-2.28;\
      wget --no-check-certificate  https://mirror.tuna.tsinghua.edu.cn/gnu/gdb/gdb-9.2.tar.xz;\
      tar -xf gdb-9.2.tar.xz && rm -rf gdb-9.2.tar.xz && cd gdb-9.2; \
      mkdir build && cd build/;\
      ../configure --prefix=/usr;\
      make -j 8 && make install;\
      cd /packages && rm -rf /packages/gdb-9.2;\
      wget --no-check-certificate https://cmake.org/files/v3.20/cmake-3.20.6-linux-x86_64.sh;\
      chmod +x cmake-3.20.6-linux-x86_64.sh;\
      ./cmake-3.20.6-linux-x86_64.sh --prefix=/usr --exclude-subdir --skip-license;\
      rm -rf /package/cmake-3.20.6-linux-x86_64.sh
ENV LC_ALL en_US.utf8
USER finance
WORKDIR /home/finance
