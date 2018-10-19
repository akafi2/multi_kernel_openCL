
CC = g++

AOCL_INCLUDE = $(shell aocl compile-config)
AOCL_LIBS    = $(shell aocl link-config)

ALTERA = -DALTERA

NAME = backprop
ifeq ($(OS),Windows_NT)
	EXE = $(NAME).exe
else
	EXE = $(NAME)
endif
SRC = backprop_ocl.cpp backprop.c facetrain.c imagenet.c

ifdef OUTPUT
	EXTRA_FLAGS += -DOUTPUT
endif

ifdef ALTERA
	ifdef HOST_ONLY
		AOT_PROGRAMS = 
	else
		AOT_PROGRAMS = $(KERNEL_ALTERA_NAMES)
	endif
else
	AOT_PROGRAMS =
endif



all: $(EXE) $(AOT_PROGRAMS)

profile: CFLAGS += -DPROFILE
profile: $(EXE) $(AOT_PROGRAMS)

$(EXE): $(SRC)
	$(CC) $(CFLAGS) $(SRC) -o $(EXE) $(AOCL_INCLUDE) $(AOCL_LIBS) $(ALTERA)

clean:
	$(RM) $(EXE) *.aoco $(KERNEL_NAMES)
