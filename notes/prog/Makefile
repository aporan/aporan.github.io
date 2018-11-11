SHELL=bash
# index file
INDEX = index.org

# gets list of all directories
DIR = $(wildcard */)

# add $(INDEX) suffix
TARGETS=$(DIR:%=%$(INDEX))

index: $(TARGETS)
	rm -f $(INDEX) && touch $(INDEX)
	for dir in $^;                                      \
	do                                                  \
	    echo "[[$$dir][$${dir%$(INDEX)}]]" >> $(INDEX); \
	done;

# attach index.org in every DIR path
# for every compilation, add an entry
# to the every dir's index file

# if any dir has Makefile, the index
# file only contains the list of dirs
# else the index file contains entries
# of articles / notes / blogs

$(TARGETS): %/$(INDEX) : %
	rm -f $^/$(INDEX) && touch $^/$(INDEX)
	for file in $(filter-out %$(INDEX),    \
			$(filter %.org,        \
			    $(wildcard $^/*)   \
			 )                     \
		     );			       \
	do                                     \
	    name=$${file#$^/};                 \
	    echo "[[$${name%.org}][$$name]]"   \
		    >> $^/$(INDEX);            \
	done;                                  \
