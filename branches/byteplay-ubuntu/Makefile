#!/usr/bin/make -f

pname:=$(shell basename `pwd`)

build: debuild

upload: clean dsc
	cd deb_dist/$(pname)*; debuild -S
	dput ppa deb_dist/*.changes

debuild: dsc
	cd deb_dist/$(pname)*; debuild

eggbuild:
	python setup.py bdist_egg
	
dsc: setup.py
	python setup.py --command-packages stdeb.command sdist_dsc

install: debuild
	sudo dpkg -i `find deb_dist -name '*.deb' | head -1`
	
clean:
	rm -rf deb_dist
	rm -rf $(pname).egg-info

remove: clean
	sudo dpkg -P python-$(pname)
