SHELL=bash
# index file
INDEX = index.org

# gets list of all directories
DIR = $(wildcard */)

# add $(INDEX) suffix
TARGETS=$(DIR:%=%$(INDEX))

.SILENT: print index $(TARGETS) clean

all: print index

print:
	echo -e "Generating index.org for SUBDIR if required"

index: $(TARGETS)
	rm -f $(INDEX) && touch $(INDEX)
	for dir in $^;                         \
	do                                     \
	    echo "[[$$dir][$${dir%$(INDEX)}]]" \
            >> $(INDEX);                   \
	done;
	echo "Generating ROOT $@.org" 

# attach index.org in every DIR path
# for every compilation, add an entry
# to the every dir's index file

# if any dir has Makefile, the index
# file only contains the list of dirs
# else the index file contains entries
# of articles / notes / blogs

$(TARGETS): %/$(INDEX) : %
	if [ -e $^/Makefile ]; then                  \
        $(MAKE) -C $^ -s index;                  \
	else                                         \
        rm -f $^/$(INDEX) && touch $^/$(INDEX);  \
        for file in $(filter-out %$(INDEX),      \
                   $(filter %.org,               \
                       $(wildcard $^/*)          \
                    )                            \
                );                               \
        do                                       \
           name=$${file#$^/};                    \
           echo -e "[[$$name][$${name%.org}]]\n" \
               >> $^/$(INDEX);                   \
        done;                                    \
    fi;                                          
	echo "  ...  $^" 

clean:
	find . -name "index.org" -type f -delete
	echo "Remove ALL index.org files"
