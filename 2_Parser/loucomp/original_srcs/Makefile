# project 1
# ./lex/tiny.l --> cminus.l

# project 2
# ./yacc/tiny.y --> ./cminus.y
# ./yacc/globals.h --> ./globals.h 

# Above files overwritten

CC = gcc
CFLAGS = 

OBJS_FLEX = main.o util.o lex.yy.o symtab.o analyze.o code.o cgen.o parse.o
OBJS_YACC = main.o util.o lex.yy.o symtab.o analyze.o code.o cgen.o y.tab.o

# .PHONY: all scanner_flex $(OBJS) $(OBJS_FLEX) lex.yy.c

all : cminus

cminus: $(OBJS_YACC)
	$(CC) $(CFLAGS) $(OBJS_YACC) -o $@

scanner_flex: $(OBJS_FLEX)
	$(CC) $(CFLAGS) $(OBJS_FLEX) -o $@ -lfl

lex.yy.o: cminus.l
	flex $^
	$(CC) $(CFLAGS) -c lex.yy.c -lfl

y.tab.o: cminus.y
	yacc -d $^
	$(CC) $(CFLAGS) -c y.tab.c -lfl

globals.h: cminus.y
	yacc -d $^

main.o: main.c globals.h util.h scan.h parse.h analyze.h cgen.h
	$(CC) $(CFLAGS) -c main.c

util.o: util.c util.h globals.h
	$(CC) $(CFLAGS) -c util.c

scan.o: scan.c scan.h util.h globals.h
	$(CC) $(CFLAGS) -c scan.c

parse.o: parse.c parse.h scan.h globals.h util.h
	$(CC) $(CFLAGS) -c parse.c

symtab.o: symtab.c symtab.h
	$(CC) $(CFLAGS) -c symtab.c

analyze.o: analyze.c globals.h symtab.h analyze.h
	$(CC) $(CFLAGS) -c analyze.c

code.o: code.c code.h globals.h
	$(CC) $(CFLAGS) -c code.c

cgen.o: cgen.c globals.h symtab.h code.h cgen.h
	$(CC) $(CFLAGS) -c cgen.c

clean:
# 	rm -vf scanner_flex *.o lex.yy.c y.tab.c y.tab.h
	rm -vf *.o y.tab.c y.tab.h
