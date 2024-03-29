COMPILER_OPTIONS?=g++ -std=c++11 -O2 -Wall -Wpedantic -Wextra -Werror
TARGET_DIR?=./bin
ADDITIONAL_LIB_DIR?=-L../../build/bin
ADDITIONAL_LIB=-ldspfft

ADDITIONAL_INCLUDE=-I../../build/include
COMPILER_ALL_OPTIONS=$(COMPILER_OPTIONS)

BIN_DIR=./bin
DEPS_DIR=./deps
RAW_OBJECTS=$(patsubst %.cpp,%.o,$(shell ls *.cpp))
TARGET_NAME=main.out
TARGET=$(TARGET_DIR)/$(TARGET_NAME)
OBJECTS=$(patsubst %.o,$(BIN_DIR)/%.o,$(RAW_OBJECTS))
DEPS=$(patsubst %.o, $(DEPS_DIR)/%.d,$(RAW_OBJECTS))

$(shell mkdir -p $(DEPS_DIR))
$(shell mkdir -p $(BIN_DIR))

.PHONY: build, debug

$(TARGET): $(OBJECTS)
	$(COMPILER_ALL_OPTIONS) -o $@ $^ $(ADDITIONAL_LIB_DIR) $(ADDITIONAL_LIB)

$(DEPS): $(DEPS_DIR)/%.d: %.cpp
	$(COMPILER_ALL_OPTIONS) $(ADDITIONAL_INCLUDE) -MM $< | sed -e 1's,^,$(BIN_DIR)/,' > $@

$(OBJECTS): $(BIN_DIR)/%.o: %.cpp
	$(COMPILER_ALL_OPTIONS) $(ADDITIONAL_INCLUDE) -o $@ -c $<

include $(DEPS)

.PHONY: clean
clean:
	-rm $(TARGET) $(OBJECTS) $(DEPS)
	-rmdir $(DEPS_DIR) $(BIN_DIR)
