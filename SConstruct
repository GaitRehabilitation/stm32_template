# Create and initialize the environment.
env = Environment()

# Set environment for AVR-GCC.
env['CC'] = 'arm-none-eabi-gcc'
env['CXX'] = 'arm-none-eabi-g++'
env['CPPPATH'] = ['/usr/avr/include/', 'build']
env['OBJCOPY'] = 'arm-none-eabi-objcopy'
env['SIZE'] = 'avr-size'
env.Append(CCFLAGS = '-g -O2 -Wall -mlittle-endian -mthumb -mthumb-interwork -mcpu=cortex-m0 -fsingle-precision-constant -Wdouble-promotion -flto')


# Set environment for an Atmel AVR Atmega 328p microcontroller.
# Create and initialize the environment.
# env.Append(CXXFLAGS = '-std=gnu99 ')
env.Append(LINKFLAGS = '-flto -ffreestanding -nostdlib')
# env.Append(LINKFLAGS = '-lm')

# Define target name.
TARGET = 'build/main'

# Define source file.
env.Append(CPPPATH=[])
sources = [
    Glob('./main.cpp')]

# Build the program.
# Default() is used so that when running scons only sources are
# compiled and linked- no other commands (see below) are run

Default(env.Program(target = TARGET + '.elf', source = sources))

# Create hex binary file.
Default(env.Command(TARGET + '.hex', TARGET + '.elf', env['OBJCOPY'] + ' -O ihex $SOURCE $TARGET'))

# Compute memory usage.
# Default(env.Command(None, TARGET + '.elf', env['SIZE'] + ' -C --mcu=' + DEVICE + ' $SOURCE'))
Default(env.Command(None, None, 'ctags -R -f src/.tags src'))
