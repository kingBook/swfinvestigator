.SUFFIXES: .cpp .c .o

NAME=as3_crypto_wrapper
PATH:=${ALCHEMY_HOME}/achacks:${PATH}
GG = gluegen
INC = -I ${ALCHEMY_HOME}/openssl/include
CC = gcc
CCPP = g++
CFLAGS = -DTERMIOS -DL_ENDIAN -fomit-frame-pointer -O3 -Wall
LDFLAGS = -L=${ALCHEMY_HOME}/openssl/lib -l=crypto
OBJS = 

.cpp.o:
	$(CCPP) $(INC) $(CFLAGS) -c $<
.c.o:
	$(CC) $(INC) $(CFLAGS) -c $<

all: $(NAME)

glue.c : $(NAME).gg
	$(GG) $(NAME).gg -oas $(NAME).as -cpackage cmodule.$(NAME) -package alchemy.samples -class $(NAME)

glue.o : glue.c

$(NAME) : glue.o $(OBJS)
	$(CC) $(INC) $(CFLAGS) -swc -o $(NAME).swc glue.o $(OBJS) $(LDFLAGS) 

clean:
	rm $(OBJS) glue.* $(NAME).swc 
	rm swfbridge.log 
	rm *achacks*
	rm -r _sb_*
