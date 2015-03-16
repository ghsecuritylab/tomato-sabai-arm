include ../common.mak

ifneq ($(wildcard $(SRCBASE)/wl/$(PLATFORM)/eapd),)
UTILS := wl nas eapd
else
UTILS := wl
endif

.PHONY: all

all: $(UTILS)

clean:
	rm -f *~ $(UTILS)

ifneq ($(wildcard $(SRCBASE)/wl/$(PLATFORM)/wl),)
wl:
	@echo [ prebuilt ] CP $@
	@cp -f $(SRCBASE)/wl/$(PLATFORM)/wl wl
else
wl: wl_exe.o
	@echo [ prebuilt ] CC $@
	@$(CC) $(CCFLAGS) -DBCMWPA2 -o $@ $<

endif

ifneq ($(wildcard $(SRCBASE)/wl/$(PLATFORM)/nas),)
nas:
	@echo [ prebuilt ] CP $@
	@cp -f $(SRCBASE)/wl/$(PLATFORM)/nas nas
endif

ifneq ($(wildcard $(SRCBASE)/wl/$(PLATFORM)/eapd),)
eapd:
	@echo [ prebuilt ] CP $@
	@cp -f $(SRCBASE)/wl/$(PLATFORM)/eapd eapd
endif

install: all
	@echo [ prebuild ] installing...
	install -d $(INSTALLDIR)/usr/sbin

ifneq ($(wildcard $(SRCBASE)/wl/$(PLATFORM)/nas),)

	install -m 0755 nas $(INSTALLDIR)/usr/sbin/nas
	$(STRIP) $(INSTALLDIR)/usr/sbin/nas
	# nas4not is now a symbolic link to nas
	ln -sf nas $(INSTALLDIR)/usr/sbin/nas4not
endif

	install -m 0755 wl $(INSTALLDIR)/usr/sbin/wl
	$(STRIP) $(INSTALLDIR)/usr/sbin/wl
	
ifneq ($(wildcard $(SRCBASE)/wl/$(PLATFORM)/eapd),)
	install -d $(INSTALLDIR)/bin
	install -m 0755 eapd $(INSTALLDIR)/bin/eapd
	$(STRIP) $(INSTALLDIR)/bin/eapd
endif

