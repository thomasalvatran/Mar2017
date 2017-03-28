# Mar2017
#define GPIO_START_ADDR 0x4804C000
#define GPIO_OE 0x134   //register for GPIO Output Enable offset 0x134
GPIO_START_ADDRESS at 0x4804C000 can be found p. 173 GPIO1 0x4804_C000 of Techincal Reference Manual
AM335x ARM Cortex-A8 Microprocessors (MPUs) Technical Reference Manual (Rev. I)

It can be found from /proc/iomem
4804c000-4804cfff : /ocp/gpio@4804c000
4804c000-4804cfff : 4804c000.gpio

When program is running it can be found /proc/$pid/maps
b6f32000-b6f34000 rw-s 4804c000 00:05 2292       /dev/mem

volatile void *gpio_addr = NULL;
int fd = open("/dev/mem", O_RDWR);  //file descriptor
gpio_addr = mmap(0, GPIO_SIZE, PROT_READ | PROT_WRITE, MAP_SHARED< fd, GPIO_START_ADDR) //using mmap file to I/O

//Offset of base address
gpio_oe_addr = gpio_addr  + GPIO_OE;

