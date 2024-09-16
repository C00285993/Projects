
AS=nasm # Assembly compiler
ASFLAGS=-f elf64 -g -F dwarf # Assembly flags for 64-bit
LD=ld # Linker
LDFLAGS=-m elf_x86_64 # Linker flags for 64-bit

SOURCES=$(wildcard ./*.asm) # Assembly source files
OBJECTS=$(SOURCES:.asm=.o) # Object files
EXECUTABLE=ProjectAdd # Name of the executable

# Default target
all: $(EXECUTABLE)

# Create executable
$(EXECUTABLE): $(OBJECTS)
	$(LD) $(LDFLAGS) $(OBJECTS) -o $@

# Compile assembly files to object files
%.o: %.asm
	$(AS) $(ASFLAGS) $< -o $@

# Clean up
clean:
	rm -f $(OBJECTS) $(EXECUTABLE)
