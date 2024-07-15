PKG = knn

$(PKG).gfn: $(PKG).inp $(PKG).spec $(PKG)_sample.inp $(PKG)_help.md
	gretlcli -e --makepkg $(PKG).inp


install: $(PKG).gfn
	echo pkg install $(PKG).gfn --local | gretlcli -b -e -
	cat $(PKG)_help.md | tee ../README.md

clean:
	rm -f $(PKG).gfn
