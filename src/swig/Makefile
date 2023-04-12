.ONESHELL:
SHELL = /bin/bash
.SHELLFLAGS += -e

MAIN_TARGET = $(SWIG_BASE)
DERIVED_TARGETS = $(SWIG) $(SWIG_DBG)

$(addprefix $(DEST)/, $(MAIN_TARGET)): $(DEST)/% :
	rm -fr ./swig-$(SWIG_VERSION) *.deb
	dget 'https://sonicstorage.blob.core.windows.net/packages/swig_3.0.12-2.dsc?sv=2015-04-05&sr=b&sig=k3eLfmWgmCz1Kx8SYcirX18FSQdJ76ifo%2B9rbJBnrf8%3D&se=2046-09-30T22%3A11%3A45Z&sp=r'

	pushd ./swig-$(SWIG_VERSION)
ifeq ($(CROSS_BUILD_ENVIRON), y)
	dpkg-buildpackage -rfakeroot -b -us -uc -a$(CONFIGURED_ARCH) -Pcross,nocheck -j$(SONIC_CONFIG_MAKE_JOBS) --admindir $(SONIC_DPKG_ADMINDIR)
else
	dpkg-buildpackage -rfakeroot -b -us -uc -j$(SONIC_CONFIG_MAKE_JOBS) --admindir $(SONIC_DPKG_ADMINDIR)
endif
	popd

	mv $(DERIVED_TARGETS) $* $(DEST)/

$(addprefix $(DEST)/, $(DERIVED_TARGETS)): $(DEST)/% : $(DEST)/$(MAIN_TARGET)
