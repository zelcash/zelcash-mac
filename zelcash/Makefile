
target_name ?= zelcash

include ../Makefile.build

ZELCASH_VERSION=1

zelcash_clone:
	if [ ! -d "zelcash_$(ZELCASH_VERSION)" ]; then git clone -b $(ZELCASH_VERSION) https://github.com/Lumiboy/zelcash.git zelcash_$(ZELCASH_VERSION); fi

zelcash_config:
	$(call patchme,zelcash_$(ZELCASH_VERSION))

zelcash_build:
	( cd zelcash_$(ZELCASH_VERSION); \
		LIBTOOLIZE=glibtoolize ./zcutil/build.sh --disable-libs; \
	)

zelcash_install:
	rm -rf tmp
	mkdir -p tmp
	mkdir -p ${BSPINSTALL}/usr/local
	make DESTDIR=${BSPROOT}/zelcash/tmp -C zelcash_$(ZELCASH_VERSION) install
	cp -af ${BSPROOT}/zelcash/tmp${BSPROOT}/zelcash/zelcash_$(ZELCASH_VERSION)/depends/*/* ${BSPINSTALL}/usr/local
# install zelcash init script
	cp -a files/* ${BSPINSTALL}/usr/local/bin

zelcash_uninstall:
	make -C zelcash_$(ZELCASH_VERSION) uninstall

zelcash_clean:
	if [ -f "zelcash_$(ZELCASH_VERSION)/Makefile" ]; then make -C zelcash_$(ZELCASH_VERSION) distclean; fi

zelcash_distclean:
	rm -rf zelcash_$(ZELCASH_VERSION)
