#include ../../common/make.config
# C compiler
CC:= g++
#CC_FLAGS := -g -O2

LDFLAGS:= -lOpenCL

SOURCES=cluster.c getopt.c read_input.c kmeans_clustering.c rmse.c

#replace all .c with .o as object files
OBJECTS:=$(SOURCES:.c=.o)

EXECUTABLE:=kmeans

all: $(EXECUTABLE)

$(EXECUTABLE): $(OBJECTS)  kmeans.cpp
	$(CC)  kmeans.cpp $(OBJECTS) -o $@ $(LDFLAGS)

.cpp.c.o:
	$(CC) $(CFLAGS) $< -o $@

#kmean: kmeans.o cluster.o getopt.o read_input.o kmeans_clustering.o rmse.o
#	$(CC) $(CC_FLAGS) -lOpenCL kmeans.o cluster.o getopt.o read_input.o kmeans_clustering.o rmse.o -o kmeans

#	$(CC) $(CC_FLAGS) -lOpenCL kmeans.cpp cluster.o getopt.o read_input.o kmeans_clustering.o rmse.o -o kmeans -I$(OPENCL_INC) -I$(OPENCL_DIR)/shared/inc/ -L$(OPENCL_LIB)

#%.o: %.[ch]
#	$(CC) $(CC_FLAGS) $< -c

#cluster.o: cluster.c
#	$(CC) $(CC_FLAGS) cluster.c -c

#getopt.o: getopt.c
#	$(CC) $(CC_FLAGS) getopt.c -c

#kmeans.o: kmeans.cpp
#	$(CC) $(CC_FLAGS) kmeans.cpp read_input.c -c

#rmse.o: rmse.c
#	$(CC) $(CC_FLAGS) rmse.c -c

clean:
	rm -f *.o *~ kmeans *.linkinfo
