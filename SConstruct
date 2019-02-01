# Create and initialize the environment.
env = Environment()

# Set environment for AVR-GCC.
env['CC'] = 'arm-none-eabi-gcc'
env['CXX'] = 'arm-none-eabi-g++'
env['OBJCOPY'] = 'arm-none-eabi-objcopy'
env['SIZE'] = 'arm-none-eabi-size'


# Declare some variables about microcontroller.
# Microcontroller type.
DEVICE = 'cortex-m4'

env.Append(CCFLAGS = '-mcpu=' + DEVICE)
env.Append(CCFLAGS = '-std=gnu99 -g -O2 -Wall -TSTM32F401VCTx_FLASH.ld')
env.Append(CCFLAGS = '-mlittle-endian -mthumb -mthumb-interwork')
env.Append(CCFLAGS = '-fsingle-precision-constant -Wdouble-promotion')
env.Append(CCFLAGS = '-mfpu=fpv4-sp-d16 -mfloat-abi=hard')
env.Append(CCFLAGS = '-DUSE_STDPERIPH_DRIVER -DSTM32F401xC')

# Define target name.
TARGET = 'build/main'

# Define source file.
sources = [
    'src/main.c',
    'src/stm32f4xx_it.c' ,
    'src/system_stm32f4xx.c',
    'src/syscalls.c' ,
    'src/config.c' ,
    'src/led.c',
    'src/stm32f4xx_hal.c',
    'src/stm32f4xx_hal_rcc.c',
    'src/stm32f4xx_hal_gpio.c',
    'src/stm32f4xx_hal_cortex.c',
    'src/startup_stm32f401xc.s', 
    Glob('lib/Drivers/STM32F4xx_HAL_Driver/Src/*.c')]

env.Append(CPPPATH=[
    'lib/Drivers/STM32F4xx_HAL_Driver/Inc',
    'lib/Drivers/CMSIS/Device/ST/STM32F4xx/Include',
    'lib/Drivers/CMSIS/Include',
    'src'])

# Build the program.
# Default() is used so that when running scons only sources are
# compiled and linked- no other commands (see below) are run

Default(env.Program(target = TARGET + '.elf', source = sources))

# Create hex binary file.
Default(env.Command(TARGET + '.hex', TARGET + '.elf', env['OBJCOPY'] + ' -O ihex $SOURCE $TARGET'))

# Compute memory usage.
Default(env.Command(None, TARGET + '.elf', env['SIZE'] + ' -tA ' + ' $SOURCE'))
Default(env.Command(None, None, 'ctags -R -f src/.tags src'))
