
target_name ?= zelcash

include ../Makefile.build

ZELCASH_VERSION=v2.0.0

zelcash_clone:
	if [ ! -d "zelcash_$(ZELCASH_VERSION)" ]; then git clone -b $(ZELCASH_VERSION) https://github.com/zelcash/zelcash.git zelcash_$(ZELCASH_VERSION); fi

zelcash_config:
	@true

zelcash_build:
	( cd zelcash_$(ZELCASH_VERSION); \
		CFLAGS="" CXXFLAGS="" LIBTOOLIZE=glibtoolize ./zcutil/build.sh -j ${BSPJOB}; \
	)

zelcash_install:
	rm -rf tmp
	mkdir -p tmp
	mkdir -p ${BSPINSTALL}/usr/local
	make DESTDIR=${BSPROOT}/zelcash/tmp -C zelcash_$(ZELCASH_VERSION) install
	cp -af ${BSPROOT}/zelcash/tmp/* ${BSPINSTALL}
	cp -a files/* ${BSPINSTALL}/usr/local/bin

zelcash_uninstall:
	make -C zelcash_$(ZELCASH_VERSION) uninstall

zelcash_clean:
	if [ -f "zelcash_$(ZELCASH_VERSION)/Makefile" ]; then make -C zelcash_$(ZELCASH_VERSION) distclean; fi

zelcash_distclean:
	rm -rf zelcash_$(ZELCASH_VERSION)
