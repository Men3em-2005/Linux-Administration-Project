#===================================================================================================
# Name        : Makefile Project
# Copyright   : Edges For Training
# Description : A Makefile to compile and link a modular program with separate source files for 
#               simple and complex operations. It organizes include directories, source directories,
#               and builds the final executable. This is just a template you can start with your
#				own Makefile (remember makefile names: Makefile - Name.mk - Name < make -f Name >)
#===================================================================================================

# Main Directories
ROOT_DIR = ..
APP_DIR = $(ROOT_DIR)/Application
MODULES_DIR = $(ROOT_DIR)/Modules

# Modules Directories
CAESAR_CIPHER_DIR = $(MODULES_DIR)/caesar_cipher
XOR_CIPHER_DIR = $(MODULES_DIR)/xor_cipher

# Application Directories
APP_OUT_DIR = $(APP_DIR)/out
APP_OBJ_DIR = $(APP_OUT_DIR)/gen
APP_LIB_DIR = $(APP_OUT_DIR)/libs
APP_BIN = $(APP_DIR)/output   # ✅ stays in Application

# Modules Source files
CAESAR_CIPHER_SRC = $(CAESAR_CIPHER_DIR)/src/caesar_encrypt.c \
                    $(CAESAR_CIPHER_DIR)/src/caesar_decrypt.c
XOR_CIPHER_SRC    = $(XOR_CIPHER_DIR)/src/xor_encrypt.c \
                    $(XOR_CIPHER_DIR)/src/xor_decrypt.c

# Modules Object files
CAESAR_CIPHER_OBJ = $(APP_OBJ_DIR)/caesar_encrypt.o \
                    $(APP_OBJ_DIR)/caesar_decrypt.o
XOR_CIPHER_OBJ    = $(APP_OBJ_DIR)/xor_encrypt.o \
                    $(APP_OBJ_DIR)/xor_decrypt.o

# Modules Library files
CAESAR_CIPHER_LIB = $(APP_LIB_DIR)/libcaesar.a
XOR_CIPHER_LIB    = $(APP_LIB_DIR)/libxor.so

# Application Source files
APP_SRC = $(APP_DIR)/app.c

# Application Object files
APP_OBJ = $(APP_OBJ_DIR)/app.o

# Compiler and tools
CC = gcc
CFLAGS = -I$(CAESAR_CIPHER_DIR)/inc -I$(XOR_CIPHER_DIR)/inc -fPIC
AR = ar rcs

#===================================================================================================
# 1) Compile and archive the caesar_cipher static library
#===================================================================================================
$(APP_OBJ_DIR)/caesar_encrypt.o: $(CAESAR_CIPHER_DIR)/src/caesar_encrypt.c
	$(CC) $(CFLAGS) -c $(CAESAR_CIPHER_DIR)/src/caesar_encrypt.c -o $(APP_OBJ_DIR)/caesar_encrypt.o

$(APP_OBJ_DIR)/caesar_decrypt.o: $(CAESAR_CIPHER_DIR)/src/caesar_decrypt.c
	$(CC) $(CFLAGS) -c $(CAESAR_CIPHER_DIR)/src/caesar_decrypt.c -o $(APP_OBJ_DIR)/caesar_decrypt.o

$(CAESAR_CIPHER_LIB): $(CAESAR_CIPHER_OBJ)
	$(AR) $(CAESAR_CIPHER_LIB) $(CAESAR_CIPHER_OBJ)

#===================================================================================================
# 2) Compile and generate the xor_cipher dynamic library
#===================================================================================================
$(APP_OBJ_DIR)/xor_encrypt.o: $(XOR_CIPHER_DIR)/src/xor_encrypt.c
	$(CC) $(CFLAGS) -c $(XOR_CIPHER_DIR)/src/xor_encrypt.c -o $(APP_OBJ_DIR)/xor_encrypt.o

$(APP_OBJ_DIR)/xor_decrypt.o: $(XOR_CIPHER_DIR)/src/xor_decrypt.c
	$(CC) $(CFLAGS) -c $(XOR_CIPHER_DIR)/src/xor_decrypt.c -o $(APP_OBJ_DIR)/xor_decrypt.o

$(XOR_CIPHER_LIB): $(XOR_CIPHER_OBJ)
	$(CC) -shared -o $(XOR_CIPHER_LIB) $(XOR_CIPHER_OBJ)

#===================================================================================================
# 3) Compile the app source file to generate the app object file
#===================================================================================================
$(APP_OBJ): $(APP_SRC)
	$(CC) $(CFLAGS) -c $(APP_SRC) -o $(APP_OBJ)

#===================================================================================================
# 4) Link them all together
#===================================================================================================
$(APP_BIN): $(APP_OBJ) $(CAESAR_CIPHER_LIB) $(XOR_CIPHER_LIB)
	$(CC) -o $(APP_BIN) $(APP_OBJ) -L$(APP_LIB_DIR) -lcaesar -lxor

#===================================================================================================
# 5) Clean the project
#===================================================================================================
clean:
	rm -rf $(APP_OUT_DIR) $(APP_BIN)

#===================================================================================================
# Default target: build everything
#===================================================================================================
all: dirs $(APP_BIN)

dirs:
	mkdir -p $(APP_OBJ_DIR) $(APP_LIB_DIR)
