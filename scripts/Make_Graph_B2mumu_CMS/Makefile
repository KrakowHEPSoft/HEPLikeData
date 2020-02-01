#----------------------------------------------------------------------
# Przyklad linkowania bibliotek systemu ROOT z wlasnym programem
#----------------------------------------------------------------------
.SUFFIXES:  .o .c .cxx .cpp .C .f .l  .s  .sh  .h  .a .cc
#======================================================================
# Biblioteki ROOTa dla linkera 
# 1) Jawnie:
##  Sciezka to systemu ROOT - nalezy ja ustawic odpowiednio 
RPATH = $(ROOTSYS)
RLIB=  -lgsl -lgslcblas  -L$(RPATH)lib -lCore -lMathMore -lHist -lGraf -lGraf3d -lGpad -lTree -lRooFitCore -lRooFit -lRooStats  -lRint -lPostscript -lMatrix -lPhysics -lm -ldl -lpthread -rdynamic -Wl,--no-as-needed $(ROOTGLIBS)
#2) Niejawnie, przy uzyciu root-config
#RLIB= `root-config --libs`
#======================================================================
# Nazwa biezacego katalogu
DIRNAME = ./
#======================================================================
# Nazwa rdzeniowa modulu programu
NAME1 = makeGraph
#NAME2 = RooIpatia2
# Pliki objectowe (po kompilacji)
OBJT1 = $(NAME1).o
#OBJT2 = $(NAME2).o 
# Pliki wykonawcze (po linkowaniu)
EXEC1 = $(NAME1).x
# Nazwa i opcje kompilatora
CXX = g++
# 1) Jawnie
#CXXFLAGS = -O -Wall -pthread -I$(RPATH)include
# 2) Przy uzyciu root-config
CXXFLAGS = -O2 -Wall  `root-config --cflags`
# Nazwa i opcje linkera
LD = $(CXX)
LDFLAGS = `root-config --ldflags`

CXXFLAGS = -O2 -Wall -w -std=c++11 `root-config --cflags` -I/usr/local/include
#EXTRALIBS += $(shell $(ROOTSYS)/bin/root-config --libs)
LDFLAGS += $(shell $(ROOTSYS)/bin/root-config --libs) 
RLIB += $(shell $(ROOTSYS)/bin/root-config --libs)

#==============================================================================
# Kompilacja dla modulow z plikami naglowkowymi
%.o: %.cxx %.h
	$(CXX) $(CXXFLAGS) -c $<
# Kompilacja dla modulow bez plikow naglowkowych
%.o: %.cxx
	$(CXX) $(CXXFLAGS) -c $<
#==============================================================================
.PHONY: all run clean tar
all: ${EXEC1}
#==============================================================================
# Linkowanie
${EXEC1}:  ${OBJT1}
	$(LD) -o $@ $(LDFLAGS) $^ $(RLIB)

#==============================================================================
# Uruchamianie
run: ${EXEC1}
	./${EXEC1}
#==============================================================================
clean:
	(rm -f *.o *.a *~ *.exe *.x core lmap *.dvi *.aux *.log a.out)
#==============================================================================
tar: clean
	(cd ../; tar -cvzf $(DIRNAME).tar.gz $(DIRNAME) )
#==============================================================================
# Wszelkie akcje jakie należy podjąć aby program zaprezentował swoje działanie:
test: run
	@echo 'Test run finished'
#==============================================================================

