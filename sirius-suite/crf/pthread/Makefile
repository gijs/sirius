CXX = g++
CXX_FLAGS  = -O3
LINK_FLAGS = -lpthread

THREADS  = 4
MODEL    = ../input/model.la
INPUT    = ../input/test-input.txt

# File names
EXEC = crf_tag
SOURCES = $(wildcard *.cpp) ../../utils/timer.o
OBJECTS = $(SOURCES:.cpp=.o)

.PHONY: all test

all : $(EXEC)
$(EXEC): $(OBJECTS) Makefile
	$(CXX) $(OBJECTS) -o $(EXEC) $(LINK_FLAGS)

# To obtain object files
%.o: %.cpp Makefile
	$(CXX) -c $(CXX_FLAGS) $(EXTRA_FLAGS) $< -o $@

# test
test: CXX_FLAGS += -DTESTING
test: all
	@./$(EXEC) $(THREADS) $(MODEL) $(INPUT)
	-@diff -q ../input/$(EXEC).baseline ../input/$(EXEC).pthread

# To remove generated files
clean:
	$(RM) -f $(EXEC) *.o ../input/$(EXEC).pthread
