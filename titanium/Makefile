include ../Makefile.inc
EXAMPLE_RESOURCES=$(shell for file in `find examples -name "pubnub.js" | grep -v build`;do echo $$file; done)
PLATFORM=Titanium

.PHONY	: all
all: build 

.PHONY	: build
build: $(PUBNUB_JS)

$(PUBNUB_JS) : $(JSON_JS) $(PUBNUB_COMMON_JS) $(PUBNUB_PLATFORM_JS)
	echo "\n\n $(PLATFORM) \n\n" 
	mkdir $(PUBNUB_DIST_DIR)

	$(ECHO) -n "// " > $(PUBNUB_JS)
	$(ECHO) $(VERSION) >> $(PUBNUB_JS)
	$(ECHO) "(function(){" >> $(PUBNUB_JS)
	cat $(PUBNUB_COMMON_JS) $(CRYPTO_OBJ_JS) $(PUBNUB_PLATFORM_JS) >> $(PUBNUB_JS)
	sed -i -e "s/VERSION/\'$(VERSION)\'/g" $(PUBNUB_JS)
	sed -i -e "s/PLATFORM/\'$(PLATFORM)\'/g" $(PUBNUB_JS)
	$(ECHO) "})();" >> $(PUBNUB_JS)
	for f in $(EXAMPLE_RESOURCES); do cp $(PUBNUB_JS) $$f ; done

.PHONY	: clean
clean:
	rm -rf $(PUBNUB_DIST_DIR)

include ../Makefile.post
