##################################################################################################
# Copyright (c) 2022-2023, Laboratorio de Microprocesadores
# Facultad de Ciencias Exactas y Tecnología, Universidad Nacional de Tucumán
# https://www.microprocesadores.unt.edu.ar/
#
# Copyright (c) 2022-2023, Esteban Volentini <evolentini@herrera.unt.edu.ar>
#
# Permission is hereby granted, free of charge, to any person obtaining a copy of this software and
# associated documentation files (the "Software"), to deal in the Software without restriction,
# including without limitation the rights to use, copy, modify, merge, publish, distribute,
# sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all copies or substantial
# portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT
# NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
# NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES
# OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
# CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
#
# SPDX-License-Identifier: MIT
##################################################################################################

##################################################################################################
# Toolchain settings
TOOLCHAIN_PREFIX ?= arm-none-eabi-

##################################################################################################
# Toolchain commands
# Preprocesor command
PP = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)gcc
# C compiler command
CC = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)gcc
# Library builder command
AR = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)ar
# Linker command
LD = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)gcc
# Assembler command
AS = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)as
# Debbuger command
GDB = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)gdb
# List simbols command
NM = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)nm
# Object dump command
OD = $(TOOLCHAIN_LOCATION)$(TOOLCHAIN_PREFIX)objdump

##################################################################################################
# Toolchain settings
# Preprocesor definitions

# Compiler flags
CFLAGS += -mthumb

# Library builder flags
AFLAGS += -mthumb

# Enable ARM Semihosting support
$(if $(findstring ENABLE_ARM_SEMIHOSTING,$(DEFINES)),\
$(eval SPECS ?= --specs=nano.specs --specs=rdimon.specs) \
$(eval LFLAGS += -l rdimon) \
, \
$(eval SPECS ?= --specs=nano.specs --specs=nosys.specs) \
)

# Linker flags
LFLAGS += -Wl,-Map="$(TARGET_NAME).map",-gc-sections,--cref
LFLAGS += -mthumb $(SPECS) -L $(MUJU) -T $(LINKSCRIPT)

# define linker extension
LD_EXTENSION = elf

# Debugger flags
GDB_FLAGS = $(TARGET_ELF) -ex "target remote localhost:3333"

# Debug server
GDB_SERVER = openocd

FLASH_WRITER = openocd
